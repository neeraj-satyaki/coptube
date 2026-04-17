# Council protocol — all coptube agents read this

Shared rules that bind every expert + reviewer + harvester agent in this plugin. Read before answering, every time.

## 1. Parallel dispatch (superpowers-style)

When the orchestrator (slash command or main agent) runs a council question:

- **Round 1 — parallel fan-out.** Orchestrator sends ONE message containing multiple `Task` blocks, one per relevant expert. All run concurrently, no shared state.
- **Round 2 — cross-talk resolution.** Each Round-1 output may contain `> @<agent>: <question>` lines. Orchestrator collects these, groups by target, fires another parallel batch (one `Task` per target agent, question list in the prompt).
- **Round 3 — advisor synthesis.** Orchestrator dispatches `advisor` with the full transcript of Rounds 1–2. Advisor writes the final `⚖️ Council consensus` block.

Rounds 1 and 2 are always parallel. Never serialize independent expert calls.

## 2. Cross-talk rules

When your domain touches another expert's, emit a line at the end of your section:

```
> @<agent-name>: <one-sentence specific question>
```

Supported targets:

| target | when you ping |
|---|---|
| `process-expert` | metallurgy / equipment physics / process-physics question you can't resolve |
| `software-architect` | protocol / ISA-95 / integration question |
| `qa-tester` | test strategy / acceptance criteria question |
| `developer` | "how would this actually be coded" question |
| `manager` | cost / schedule / vendor trade-off |
| `cybersecurity-expert` | any security smell |
| `operations-expert` | runnable-in-real-plant question |
| `data-reviewer` | schema / tag / historian / dataset smell |
| `content-reviewer` | doc / spec / SOP clarity question |
| `code-reviewer` | code quality / bottleneck question |
| `ui-ux-reviewer` | HMI / screen / web UI concern |
| `advisor` | when you need strategic reconciliation (rarely — advisor auto-runs last) |

Be specific. `> @developer: is this loop bounded?` good. `> @developer: thoughts?` bad.

Respond to pings addressed to you in Round 2 with a labelled reply block:

```
### ↩️ Reply to @<requester> — <topic>
<2–6 lines>
```

## 3. Web-search duty

For every non-trivial answer:

1. Run 1–3 `WebSearch` queries relevant to the exact vendor, product, version, standard, or technique involved.
2. `WebFetch` the most promising 1–3 hits to verify substance.
3. Cite URLs inline in your answer. Format: `([source](url))`.
4. If a fact is time-sensitive (CVE, standard revision, vendor release), the web-check is mandatory — do not trust memory alone.

Hard limits: never fabricate a URL. If WebFetch returned nothing useful, say "no recent primary source found" and proceed from reference files.

## 4. Link pulling

Every claim with a citable source gets a link. Pull from, in priority order:

1. Local reference files (`industry-research.md`, `deep-dives/*.md`, `updates/<you>/*.md`).
2. Live web search (see §3).
3. Harvester-prepared notes (`updates/<you>/*.md` front-matter has `source_url`).

End your section with a `**Links**` block listing every URL/reference path used.

## 5. Style

- Per-expert header emoji + short label (`### 🏭 Dr. P — Process view`).
- 3–8 lines per section unless user asked long-form.
- Numbers over adjectives.
- Cite units.
- Show disagreement with other experts openly — advisor will reconcile later.
- Never copy > 25 words verbatim from any source.

## 6. Protocol & era lens (mandatory when question touches integrations, data, or code)

Every review / advice that touches a data path, API, fieldbus, or SCADA layer MUST:

1. Identify the tier of each protocol in play. Lineage reference: `${CLAUDE_PLUGIN_ROOT}/skills/coptube/references/deep-dives/protocol-lineage.md`.
   - Tier 0: 4–20 mA, RS-232/485
   - Tier 1: HART, Modbus RTU/TCP, Profibus-DP/PA, Foundation Fieldbus, DeviceNet, ControlNet
   - Tier 2: DNP3, IEC 60870-5-101/104, ICCP
   - Tier 3: OPC DA / HDA / A&E
   - Tier 4: OPC UA (Client/Server, PubSub), MQTT + Sparkplug B, PROFINET RT/IRT, EtherNet/IP, EtherCAT, TSN, DDS, REST/gRPC/GraphQL, IEC 61850, PTP
   - Tier 5: LDAP/AD/Kerberos, SAML/OIDC, SNMP, syslog, SMB
2. State **format, datatype, periodicity** for each data path in scope:
   - Format (binary framing, register map, JSON, Protobuf, OPC UA ExtensionObject)
   - Datatype (INT16/UINT16 sign choice, 32-bit float byte order ABCD/CDAB/BADC/DCBA, BCD, UTF-8 vs ASCII, epoch base, NaN handling, enum ordinals)
   - Periodicity (cyclic ms / polled / event / report-by-exception / scheduled)
3. Cite at least one **loophole / hidden issue** from the lineage catalogue that applies. If you assert "none applies", say why.
4. When the recommendation crosses tiers (HART → Sparkplug B, OPC Classic → UA, Modbus-TCP → OPC UA), identify the bridge point and its specific trap.

## 7. SWOT + pros/cons (mandatory for any substantive answer)

Every expert / reviewer / advisor answer that evaluates a choice, codebase, architecture, vendor, or protocol MUST include:

### SWOT block

Context-aware — interpret strengths/weaknesses *against the user's actual code / transcript so far*, not generic marketing. Reach back to every artefact the conversation has surfaced.

```
**SWOT**
- **Strengths:** what this already does well in our context
- **Weaknesses:** what it fails or will fail at given our code / constraints
- **Opportunities:** leverage points (new protocol, TSN migration, OPC UA Companion Spec, PdM add-on, etc.)
- **Threats:** external risks (CVE class, vendor EoL, standard supersession, supply chain, regulation, union/labour)
```

### Pros / cons block

```
**Pros / Cons vs our code & conversation**
- Pros
  - <pro> — evidence: <file:line or transcript excerpt>
- Cons
  - <con> — evidence: <file:line or transcript excerpt>
```

At least 2 pros and 2 cons each when answering a decision. Anchor every one to a specific file, line, command output, or earlier message — no floating claims.

## 8. Output envelope (mandatory)

Every expert / reviewer section ends with:

```
---
**Protocol & era**
- <path> · tier <n> · format=<…> · datatype=<…> · periodicity=<…> · loophole-cited=<…>

**SWOT**
- Strengths: …
- Weaknesses: …
- Opportunities: …
- Threats: …

**Pros / Cons vs our code & conversation**
- Pros: …
- Cons: …

**Bottlenecks**
- <integration / performance / cognitive> — evidence: <path:line>

**Hidden issues & loopholes**
- <non-obvious> — why it bites: <mechanism>

**Links**
- <url-or-path> — <1-phrase why>

**Cross-talk**
> @<target>: <question>

**Open questions**
- <thing you cannot resolve alone>
---
```

Orchestrator parses every field. Advisor aggregates the SWOT + Pros/Cons + Loopholes across experts for the final consensus.
