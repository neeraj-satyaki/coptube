# Industrial protocol lineage — legacy → modern

Span of protocols an expert must recognise in any real plant. Every review, audit, integration call must map existing traffic onto this lineage before recommending change. Old protocols rarely die — they get tunnelled, bridged, or wrapped.

## Lineage map

### Tier 0 — field wiring (analogue + early digital)

| Protocol | Era | Role | Format / datatype | Periodicity | Loopholes / hidden issues |
|---|---|---|---|---|---|
| 4–20 mA current loop | 1950s– | Sensor → controller analogue | Current (mA), linearised in DCS | Continuous | Break detection only via 3.6 / 21.5 mA band; burn-out direction (upscale vs downscale) often wrong; HART riding on loop is silent to old DCS |
| 0–10 V / 1–5 V | 1950s– | Same | Voltage | Continuous | Ground loops; long-run voltage drop; noise pickup without shielded+twisted |
| RS-232 | 1960s– | Point-to-point serial | ASCII or binary frames | As polled | No intrinsic addressing; 15 m max; no framing robustness |
| RS-485 / RS-422 | 1970s– | Multidrop serial | Same | Polled | Biasing/termination errors = silent data corruption; 32-node limit without repeater |

### Tier 1 — legacy fieldbus

| Protocol | Era | Role | Format / datatype | Periodicity | Loopholes / hidden issues |
|---|---|---|---|---|---|
| HART (Highway Addressable) | 1989– | Digital on 4–20 mA loop | 1200 baud FSK, 0–255 cmd set; 32-char device tag | Burst 1–4 Hz or poll | Host rarely polls beyond PV; secondary variables "exist" but unused; HART-IP bridges leak to IT |
| Modbus RTU / ASCII | 1979– | Serial master-slave | 16-bit registers (FC 03/04/06/16); coils (1-bit) | Polled, typ 100–500 ms | No timestamp, no quality, no auth; big/little-endian mismatch silent; 0- vs 1-based register address off-by-one |
| Modbus TCP | 1999– | Same over TCP/502 | Same registers + MBAP header | Polled | Unauth by spec; spoof trivial; no encryption; gateway to RTU preserves vulnerabilities |
| Profibus-DP | 1989– | Cyclic I/O, 9.6 kbps–12 Mbps | Fixed-length byte arrays (GSD-defined) | 1–10 ms | Token-passing fragility; station-fail silent until watchdog; long trunks need repeaters; DPV1 diag messages often ignored |
| Profibus-PA | Fieldbus for HART-grade | MBP (31.25 kbps) | 5-byte FF blocks | 250 ms–1 s | Segment power budget; safety (PA-Profile-Safety) rarely enabled |
| Foundation Fieldbus H1 | 1996– | Process plant fieldbus | Function-block, scheduled + unscheduled | 50 ms–2 s LAS schedule | Macrocycle jitter; block mode shedding silent; vendor FB libs diverge |
| DeviceNet / CIP | 1994– | CAN-based device I/O | Assembly objects, EDS | 2–10 ms | Node guarding vs heartbeat mixing; EDS drift |
| ControlNet | 1997– | Deterministic LAN | CIP over CTDMA | 0.5–100 ms NUT | End-of-life since 2020; spares scarce; taps/terminators finicky |
| AS-i | 1994– | Sensor-level | 4 bits I + 4 bits O per slave | 5 ms/31 slaves | Addressing by handheld loses trace; master firmware drift |
| INTERBUS | 1987– | Ring fieldbus | Summation frame | 1–5 ms | Ring break halts all; Phoenix Contact-specific tooling |
| CC-Link | 1996– | Mitsubishi | Cyclic + transient | 1–10 ms | Vendor-locked; bridging to non-Mitsubishi costs determinism |

### Tier 2 — legacy SCADA / telecontrol

| Protocol | Era | Role | Datatype | Periodicity | Loopholes |
|---|---|---|---|---|---|
| DNP3 (serial + IP) | 1993– | Utility SCADA, RTU → master | Class 0/1/2/3 points; timestamped events | Event-driven + integrity poll | Unauth default; Secure Authentication v5 (SAv5) rarely deployed; time-sync by DNP vs NTP collisions |
| IEC 60870-5-101 | 1995– | Utility serial telecontrol | ASDU type-ids | Cyclic + event | Same auth issues; config via spreadsheets |
| IEC 60870-5-104 | 2000– | IP version of 101 | TCP/2404, ASDU | Spontaneous + cyclic | Plaintext by default; IEC 62351 add-on rarely used |
| ICCP / TASE.2 | 1996– | Control-centre-to-control-centre | Bilateral tables | Scheduled | Access management poorly audited |
| Modbus-over-serial-radio | 1990s– | Remote wellhead / substation | Registers | Slow poll | Weak RF discipline; replay trivial |

### Tier 3 — OPC Classic

| Protocol | Era | Role | Datatype | Periodicity | Loopholes |
|---|---|---|---|---|---|
| OPC DA (Data Access) | 1996 | Tag read/write | VARIANT, quality, timestamp | Poll / subscription | DCOM pain (firewalls, auth), Windows-only, no built-in security |
| OPC HDA (Historical) | 2001 | Historical pull | Timestamped samples | Query | Aggregation semantics vary per vendor |
| OPC A&E (Alarms & Events) | 2002 | Alarm stream | Condition/event | Subscription | No schema standardisation beyond OPC spec — vendor fields diverge |
| OPC UA (IEC 62541) | 2006+ | Unified modern replacement | Structured types, AddressSpace, Companion Specs | Polling + PubSub | Misconfigured SecurityPolicy=None, CertificateStore neglect, anonymous Users allowed, large AddressSpace DoS |

### Tier 4 — modern / convergent

| Protocol | Era | Role | Datatype / format | Periodicity | Loopholes / hidden issues |
|---|---|---|---|---|---|
| OPC UA Client/Server | 2006→ | General-purpose OT | Binary (UA-TCP) or HTTPS; Companion Specs for domain | Poll + subscription (min 50 ms typ) | Large monitored-item counts kill server; Browse DoS; certificate lifecycle |
| OPC UA PubSub (UADP + JSON) | 2018→ | Broker-less/ broker-based events | UDP multicast (UADP) or MQTT/Kafka (JSON) | 1 ms–1 s | PubSub security profiles poorly understood; JSON encoding heavy; UADP firewall issues |
| MQTT 3.1.1 / 5.0 | 2014 / 2019 | Broker pub/sub | User-defined payload | Event-driven | Topic sprawl without governance; retain-flag misuse; QoS2 rarely needed |
| Sparkplug B | 2016→ (Eclipse 2019+) | MQTT payload + state | Protobuf NBIRTH/NDATA/DBIRTH/DDATA/NDEATH | Report by exception + rebirth | Single-writer rule violated silently; primary-host STATE topic race; payload evolution breaks old consumers |
| MQTT over TLS | 2019+ | Secure broker | Same | — | Mutual-TLS rarely enforced; client-cert rotation missing |
| AMQP 1.0 | 2012 | Queue/topic | Binary | Event | Overhead vs MQTT; not common in plants |
| Apache Kafka | 2011→ | Durable log | JSON/Avro/Protobuf | Stream | Schema-registry drift; compaction vs retention confusion; topic partitioning skew |
| PROFINET IO RT / IRT | 2003/2006 | Deterministic Ethernet | Cyclic IO + acyclic record | 250 µs–1 ms IRT, 1–4 ms RT | Requires managed switches; topology detection (LLDP) mandatory; safety via PROFIsafe often misrouted |
| EtherNet/IP (CIP) | 2001 | Rockwell Ethernet | Assembly objects | 1–100 ms RPI | CIP Security (2020) rarely deployed; explicit messaging mixed with implicit |
| EtherCAT | 2003 | Summation-frame Ethernet | Process data + mailbox | 100 µs–1 ms | One master only; distributed-clocks mis-sync |
| SERCOS III | 2007 | Motion | Ring | 31.25 µs+ | Niche; motion-centric |
| CC-Link IE TSN | 2018 | Mitsubishi TSN | Cyclic + msg | 31.25 µs | Vendor-locked |
| TSN (IEEE 802.1) | 2018+ | Deterministic Ethernet substrate | 802.1Qbv/CB/AS | Microseconds | Config complexity; interoperability across switch vendors real barrier |
| DDS (OMG) | 2004, adopted in robotics, defence, industrial | Data-centric PubSub | IDL-typed samples | 10 µs+ | QoS matrix huge; misconfigured durability leaks memory |
| REST / HTTPS / JSON | 1999+ (REST 2000) | MES/ERP APIs | JSON / XML | Request-response | Pagination inconsistency; retry semantics not idempotent; webhook reliability |
| gRPC | 2016+ | Service-to-service | Protobuf | Uni/streaming | HTTP/2 proxy quirks; keepalive tuning |
| GraphQL | 2015+ | API façade | Schema | Request | N+1 on resolvers; auth at resolver level inconsistent |
| IEC 61850 (substation) | 2003+ | Substation automation | GOOSE (multicast L2), MMS (TCP), SV | GOOSE sub-ms, MMS event | Different worlds than tube plants, but often in utility infra around the plant; time-sync by PTP (IEEE 1588) critical |
| PTP IEEE 1588v2 / 2.1 | 2008 / 2019 | Time sync | BMCA | Sub-µs | Boundary-clock vs transparent-clock mix kills accuracy; PPS wiring discipline |
| NTP | 1985 | Time sync | — | ms | Plant often runs unauthenticated pool.ntp.org — single point of drift |

### Tier 5 — IT / cloud adjacency

| Protocol | Role | Hidden issues when bridged into OT |
|---|---|---|
| LDAP / AD / Kerberos | AuthN | DC unreachable during plant-LAN isolation → screens lock |
| SAML / OIDC / OAuth2 | Web AuthN | Token lifetimes vs shift length; refresh flow on air-gap |
| SNMP v2c / v3 | Device mon | v2c community string in clear; v3 underused |
| syslog / CEF / LEEF | Log shipping | UDP loss on peak; TLS rarely enabled |
| NetFlow / IPFIX | Flow data | Cardinality explosion at plant |
| SMB / CIFS | File share | SMBv1 lingering on old HMIs; ransomware surface |
| WebSocket / SSE | Live dashboards | Reverse proxy idle-timeout; reconnection storms |

## Integration patterns (and their traps)

- **Modbus → OPC UA gateway** — preserves the lack of timestamp/quality unless gateway synthesises. Byte-order config is the top source of silent wrong values.
- **OPC Classic → OPC UA wrapper** — DCOM still inside the server; DCOM hardening (March 2023 rollout) broke many.
- **MQTT Sparkplug B next to OPC UA PubSub** — two state models; primary-host concept vs session restore; if both published to same historian, duplicate or lost series.
- **PROFINET inside a plant, EtherNet/IP on another line** — physical separation recommended; CIP-over-PROFINET bridges exist but add latency.
- **Historian pulling from PLC over OPC DA AND from SCADA over SQL** — writes collide on timestamp key.
- **MES polling ERP over REST AND receiving ERP webhooks** — idempotency key required or orders double-process.
- **Historical backfill via OPC HDA + live subscribe via OPC UA** — boundary overlap causes double samples.

## Format / datatype pitfalls (always check)

- INT16 vs UINT16 — Modbus signed/unsigned choice is per-tag, often guessed.
- 32-bit float across two Modbus registers — byte/word order (ABCD, CDAB, BADC, DCBA). Vendor default ≠ plant default.
- BCD on older drives; IEEE-754 everywhere else.
- String length + encoding (ASCII vs UTF-8) — UA supports UTF-8, OPC Classic mostly ASCII; garbled tag descriptions when bridging.
- Epoch base — Windows file time (100 ns since 1601), Unix (s since 1970), OPC UA DateTime (100 ns since 1601, UTC). Mixing these silently skews by years.
- Timestamp precision — historian stores ms, PLC produces 100 ms tick; finer-grained events get clamped.
- Enum ordinals — vendor reorders between firmware revs; "state = 3" meaning drifts.
- Floating-point NaN propagation — PLC tag publishing NaN to OPC UA → subscribers crash depending on stack.
- Endianness — not just Modbus; also PROFINET raw I/O where GSDML mapping is mis-declared.

## Periodicity / sampling pitfalls

- Sampling rate < 2× phenomenon bandwidth = aliasing (Nyquist). Vibration at 1 s useless for bearings.
- Deadband (PI swinging-door) compresses transients; aggressive defaults hide process drift.
- Report-by-exception (Sparkplug) with no heartbeat = consumer can't tell "nothing happened" from "connection dead".
- Poll rate vs scan rate mismatch: SCADA polls at 500 ms, PLC toggles a bit for 100 ms — lost edge.
- Shift-boundary aggregation that double-counts if retention + compaction boundaries overlap.
- Daylight-saving — some historians keep local time → lose/duplicate 1 hour twice a year.

## Loopholes / hidden issues catalogue

1. Modbus gateway with default Unit ID = 1, production device also at Unit ID = 1 → overlapping writes.
2. OPC UA session reuse across clients — shared SubscriptionId, deletion cascades.
3. PROFINET topology-planned vs topology-detected mismatch → failover routes silently wrong.
4. Sparkplug primary-host STATE retained = true but broker restarted without session-persist → ghost primary.
5. MQTT QoS2 used "for safety" on high-rate tags → broker choke under load.
6. Kafka key = tagName → hot partitions; key = site+tag better.
7. OPC UA Certificates auto-accepted on first-use → any rogue client trusted.
8. HART-IP gateway exposing field devices over routable network — 1990s HART auth model meets internet.
9. Time drift on PLC (no NTP) → historian timeline bogus; forensic lost.
10. DCS → historian "last-good-value hold" during comms loss → stuck value indistinguishable from true stability.
11. Digital twin pulling from UNS AND directly from PLC → two sources of truth diverge 10 s under load.
12. IEC 60870-5-104 on plant WAN without encryption when utility interconnects the plant substation.
13. Safety PLC variables tunnelled through non-safety gateway → ISO 13849 / IEC 61508 audit trail broken.
14. REST API exposes integer order-ID — enumeration attack silent without rate-limit.
15. Rolling-window aggregation defined in UTC but displayed in local — report boundary off by ±1 h.

## How to use this file

Every review / advice / council answer that touches protocols MUST:

1. Identify the existing protocol layer (tier 0–5) before proposing change.
2. List format / datatype / periodicity for each data path in scope.
3. Cite at least one loophole from the catalogue above that applies (or explicitly state why none does).
4. If the recommendation crosses tiers (e.g. HART → Sparkplug B), show the bridge point and its specific trap.

Cite as: `(see deep-dives/protocol-lineage.md §Tier X / §Loopholes)`.
