---
description: Harvest books, PDFs, EPUBs, papers, blogs on a topic and file notes to the right expert. Usage:/coptube:harvest <topic|expert:all>
argument-hint: <topic> | expert:<name> | all
allowed-tools: Task
---

Dispatch the `knowledge-harvester` subagent with `$ARGUMENTS` as the brief.

## Argument forms

- `/coptube:harvest cold pilger tooling wear` → single topic, auto-route
- `/coptube:harvest expert:cybersecurity-expert recent OT CVEs in Siemens S7` → target one expert
- `/coptube:harvest all` → harvester picks one gap per expert and fills it
- `/coptube:harvest url:https://example.com/paper.pdf` → ingest a specific URL

## Dispatch

Call `Task` with `subagent_type: knowledge-harvester` and pass `$ARGUMENTS` verbatim plus instruction to follow its own workflow (search → fetch → classify → write → index → report).

Return the harvester's summary to the user unchanged.
