# Test 2a — Parallel council: software-architect

**Prompt:** S7-1500 PLC emitting process tags over Modbus TCP on plant VLAN 20. MES wants to subscribe those tags from a new OPC UA historian on a Linux VM in DMZ. Top 3 silent failure modes.

**Subagent:** coptube:software-architect
**Mode:** parallel (launched alongside coptube:cybersecurity-expert)
**Duration:** 135.0 s
**Tokens:** 20,667
**Tool uses:** 9 (loaded refs + web search + protocol-lineage.md deep-read)

---

### 🏗️ Arch — Architecture view

**Setup as drawn:** L1 Siemens S7-1500 on plant VLAN 20 → **Modbus TCP/502** (Tier 1, polled, no timestamp/quality/auth) → conduit crossing L2/L3.5 DMZ boundary → **OPC UA historian** (Tier 4) on Linux VM. The bridge is the silent-failure zone — Modbus TCP is unaware it is being consumed by a structured-type client.

**Top 3 silent failure modes:**

1. **Byte/word-order mis-declaration on 32-bit floats** (ABCD vs CDAB vs BADC vs DCBA). S7-1500 natively serves REAL as big-endian (ABCD); many Modbus TCP client libraries on Linux default to CDAB ("word-swapped big-endian") because that is the PLC5/ControlLogix legacy. Roll-force 1,842 kN silently becomes `6.3e-37` or `NaN` on the historian, trends plot a flatline near zero, and nobody notices until a quality audit — the subscription is "working", values are "valid". Same class bites INT32 counters and DINT timestamps. *(lineage.md line 100–108)*

2. **Fabricated timestamps from the gateway/client, not the PLC scan.** Modbus has no timestamp field — the OPC UA historian stamps on arrival in DMZ. Poll period at 1 s, PLC scan at 20 ms, a 100 ms toggle on a pilger-mandrel-forward bit is aliased away entirely (*lineage.md line 115*). Worse: if the DMZ VM's NTP drifts (no PTP across VLAN 20 → DMZ firewall), all historised events skew by seconds vs. the L1 event log, and post-mortem correlation of a cobble becomes impossible. The historian shows "quality=Good" the whole time.

3. **Unit ID / register-map aliasing + stale-value masquerade.** Modbus TCP has no intrinsic subscription — the OPC UA server on the Linux VM polls and republishes as monitored items. If the PLC loses the tag update (PN/DP peripheral fault, partial DB write, or PUT/GET disabled mid-life), the Modbus register holds the **last good value**. The OPC UA layer will happily report `StatusCode=Good, ServerTimestamp=now` forever. No `Bad_NoCommunication` propagates north because Modbus doesn't have a quality code to translate. Add the classic Unit ID=1 collision if any downstream gateway is chained (*lineage.md line 121*), and two devices write the same tag.

**Honourable mention (4th):** the DMZ firewall rule for TCP/502 is usually opened **bidirectionally** ("allow VLAN20 ↔ DMZ") instead of DMZ-initiated-only — Modbus TCP is unauth-by-spec, so any compromised Linux VM writes coils into a live pilger PLC.

---

**Protocol & era**
- PLC → historian · Tier 1 Modbus TCP (port 502) → Tier 4 OPC UA (binary, UA-TCP 4840) · format=16-bit register array / OPC UA ExtensionObject · datatype=INT16/UINT16/REAL word-order-dependent, no quality, no timestamp · periodicity=polled 500 ms–2 s cyclic, republished as OPC UA Subscription · loophole-cited=lineage.md line 90 + 100 + 115 + 121

**SWOT**
- Strengths: S7-1500 Modbus TCP server mature (SIMATIC MB_SERVER); OPC UA historian on Linux = vendor-neutral seam; DMZ placement aligns with IEC 62443 zone/conduit.
- Weaknesses: Modbus TCP chosen over S7-1500's native OPC UA server (built-in since FW 2.0) — self-inflicted downgrade from Tier 4 to Tier 1.
- Opportunities: Enable the S7-1500's built-in OPC UA server (needs Medium Memory Card + runtime licence) — collapses the bridge.
- Threats: IEC 62443-3-3 audit flags unauth Modbus TCP across a zone boundary; customers demand signed/encrypted OT traffic.

**Pros / Cons vs conversation**
- Pros
  - Fastest PoC path — no OPC UA server engineering on the PLC.
  - DMZ Linux VM respects ISA-95 L3.5, decouples MES lifecycle from PLC firmware.
- Cons
  - L1→DMZ skips L2 — no SCADA/historian-local buffer, DMZ firewall flap = silent gap.
  - Two semantics (registers vs UA NodeIds) = tag-alias file owned by nobody; year 3 the pilger team cannot trace which register feeds which NodeId.

**Bottlenecks**
- Modbus polling on a single TCP connection scales poorly beyond ~200 registers at 500 ms — pilger mill easily has 500+ tags; MB_SERVER FB is single-connection per instance.
- DMZ firewall = cognitive bottleneck — every new tag = register-map change + UA NodeId update + firewall re-justification.

**Hidden issues & loopholes**
- Sign of 16-bit torque reading: INT16 published, UINT16 consumed → reverse-roll torque wraps to 60000+ and analytics sees a phantom spike.
- TCP half-open: S7 FB crashes but TCP socket stays open with keepalive off — historian holds values indefinitely. Fix: SO_KEEPALIVE + heartbeat register (monotonic counter) with freeze alarm.
- VLAN 20 → DMZ stateful TCP without Modbus DPI → FC06/16 write-register from a compromised VM reaches the PLC.

**Links**
- `skills/coptube/references/deep-dives/protocol-lineage.md` lines 21–22, 90, 100–115, 121
- `skills/coptube/references/02-software-architect.md` §Protocols and their fit
- Siemens S7-1500 docs: support entries 102020340, 109755846

**Cross-talk**
> @cybersecurity-expert: Is stateful-only DMZ rule on TCP/502 (no Modbus-aware DPI) acceptable under plant's 62443-3-3 SL-T, or does pilger zone need function-code filtering (Claroty/Nozomi/Palo Alto Industrial)?
> @data-reviewer: If we stand up the historian now with DMZ-arrival timestamps, what's the retention/backfill strategy when we later switch to S7-1500 native OPC UA with real SourceTimestamps — duplicate-series risk on timestamp key?
> @developer: On the Linux VM's Modbus client (libmodbus/pymodbus/Kepware), what's the default 32-bit REAL byte order, and will you expose it as explicit config in the tag-map rather than relying on driver defaults?

**Open questions**
- S7-1500 internal OPC UA server already licensed (runtime licence ~EUR 700–1600, Memory Card ≥ 12 MB)? If yes, the Modbus TCP bridge is an unforced error.
- Does MES want write-back (setpoints, recipe, roll-pass)? Write FCs over DMZ→L1 is a different risk class than read-only.
- Actual tag count + fastest sample? Pilger stroke 80–150/min → 400–750 ms period; thrust needs ≤100 ms. Below 200 ms polling over DMZ hop will jitter.
