---
description: Process everything in updates/_inbox/ and route each note to the right expert folder.
allowed-tools: Task
---

Dispatch `knowledge-harvester` with directive: "distribute inbox". Harvester will re-score routes, move files, and update per-expert READMEs.

Pass any extra hint from `$ARGUMENTS` (e.g. `prefer: cybersecurity-expert`).
