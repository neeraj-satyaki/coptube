---
description: Audit all harvested notes for stale URLs, broken links, and malformed front-matter.
allowed-tools: Task
---

Dispatch `knowledge-harvester` with directive: "audit". Harvester walks every `updates/<expert>/*.md`, flags:

- `source_url` 404 / timeout (WebFetch check)
- `harvested_at` > 18 months AND `relevance: high` → refresh candidates
- Missing required front-matter keys
- Orphan files (not listed in expert README)

Report: `{stale: N, broken: N, malformed: N, orphan: N}` + per-expert breakdown. Do not auto-fix unless `$ARGUMENTS` contains `--fix`.
