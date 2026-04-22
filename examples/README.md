# coptube plugin — install test run

**Date:** 2026-04-17
**Install path:** `C:\Users\iotwi\.claude\plugins\cache\coptube\coptube\0.1.0\`
**Reload output:** `Reloaded: 83 plugins · 60 skills · 25 agents · 24 hooks` (agents went from 10 → 25 after install, +15 coptube agents)

## Tests run

| # | File | Subagent(s) | Mode | Duration | Tool uses | Verdict |
|---|---|---|---|---|---|---|
| 1 | `01-process-expert-cuni-preheat.md` | process-expert | solo | 32.7 s | 0 | Pass — SWOT + pros/cons + cross-talk + refs loaded |
| 2a | `02-parallel-architect.md` | software-architect | parallel with 2b | 135.0 s | 9 | Pass — loaded protocol-lineage.md, pinged @cyber + @data + @dev |
| 2b | `02-parallel-cybersecurity.md` | cybersecurity-expert | parallel with 2a | 92.6 s | 6 | Pass — live WebSearch pulled 3 unpatched 2025 S7-1500 CVEs |

## What worked

- **Parallel execution** — 2 agents dispatched in one Agent call each, ran concurrently on same question, returned distinct lenses. Architect finished in 135 s, Cyber in 92 s, end-to-end wall clock ~135 s (not 135+92).
- **Council protocol compliance** — both parallel agents produced the full envelope: Protocol & era, SWOT, Pros/Cons, Bottlenecks, Hidden issues & loopholes, Links, Cross-talk, Open questions. Matches `agents/_shared/council-protocol.md`.
- **Reference loading** — both cited `deep-dives/protocol-lineage.md` with specific line numbers (21–22, 90, 100–115, 121). Real reads of the file, not paraphrase.
- **Live web search** — Cyber ran 6 tool calls including WebSearch + WebFetch, pulled three **unpatched** 2025 S7-1500 CVEs with CVSS scores and Tenable URLs. Not in training data.
- **Cross-talk discipline** — Architect pinged `@cybersecurity-expert`, `@data-reviewer`, `@developer`. Cyber pinged `@software-architect`, `@developer`. Registered agent names (except Dr. P in test 1, which improvised non-registered role names — minor drift).
- **Protocol-era lens** — both correctly identified Tier 1 (Modbus TCP) → Tier 4 (OPC UA) bridge, cited loophole from catalogue.
- **SWOT + pros/cons context-aware** — anchored to the prompt scenario (pilger mill, DMZ VM, India), not generic.

## Observations / drift

- Dr. P (test 1) cross-talked to `@Met-Lead`, `@QC`, `@Maintenance` — these are not registered coptube subagents. Protocol says only use registered agent names. Minor.
- No agent yet validated by round-2 cross-talk resolution — that requires orchestrator (main Claude) to parse pings and fire round 2. Not tested here.
- No advisor synthesis yet — would require a 3rd dispatch with both outputs concatenated. Skipped to keep test lean.

## Next tests worth running

- `/coptube:council <question>` — full 7-expert fan-out + cross-talk round 2 + advisor
- `/coptube:company <url>` — validate WebFetch scraping + dossier write
- `/coptube:harvest <topic>` — knowledge-harvester writes to updates/<expert>/
- `/coptube:review all <path>` — 4 reviewers in parallel on a real artefact

## Conclusion

Plugin installed, reloaded, agents callable, council protocol followed, parallel dispatch works, live web-search works, reference files load from installed cache path. Ready for real use.
