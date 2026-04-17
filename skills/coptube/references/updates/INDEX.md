# Updates index

Fresh research harvested by the `knowledge-harvester` agent, routed per expert. Experts read their own subdir during every answer (newest first).

## Routing map

| Expert | Subdir | Accepts |
|---|---|---|
| Dr. P — Process | `process-expert/` | Metallurgy papers, extrusion/pilger/drawing research, ECT/UT physics, annealing kinetics, ASTM/EN/JIS updates |
| Arch — Architect | `software-architect/` | OPC UA spec releases, ISA-95 v3 updates, UNS patterns, vendor whitepapers on MES/L2 integration, digital twin reference architectures |
| Quinn — QA | `qa-tester/` | FAT/SAT checklists, GAMP 5 guidance, ISO 13849 changes, NDT qualification (ISO 9712), acceptance-criteria templates |
| Dev — Developer | `developer/` | PLC language tutorials, Ignition modules, TIA/Studio 5000 release notes, OPC UA .NET/Python client patterns, HMI UX research |
| Mgr — Manager | `manager/` | CAPEX market data, copper-price outlook, PLI notifications, tender templates, vendor post-mortems |
| Cyber — Security | `cybersecurity-expert/` | IEC 62443 part releases, OT CVEs (Siemens ProductCERT, Rockwell PSIRT, Schneider SEVD), MITRE ATT&CK for ICS, CISA advisories |
| Ops — Operations | `operations-expert/` | CMMS workflow papers, SMRP body of knowledge, PdM algorithm research, energy-per-tonne benchmarks, operator-training studies |

## Naming convention

`YYYY-MM-DD__<short-slug>__<source-domain>.md`

Example: `2026-04-17__opc-ua-1.05-safety__opcfoundation.org.md`

## Front-matter every update file must carry

```yaml
---
harvested_at: 2026-04-17
source_url: https://…
source_type: pdf | epub | blog | paper | spec | standard | book-chapter
title: "..."
authors: ["..."]
expert_routes: [process-expert, software-architect]  # one or more
relevance: high | medium | low
license_note: "CC-BY-4.0 | vendor brochure — paraphrase only | public standard summary"
---
```

## Inbox

Unrouted items go to `_inbox/` with the same naming convention. Harvester flags them for human or `/coptube:distribute` re-routing.
