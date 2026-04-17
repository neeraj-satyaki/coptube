---
description: Review target with one or all reviewers. Usage:/coptube:review <kind> <target> — kind=data|content|code|ui|all
argument-hint: <kind> <target>
allowed-tools: Task
---

Parse `$ARGUMENTS`. First token = kind. Rest = target (file path, URL, directory, pasted content).

| Kind aliases | Subagent |
|---|---|
| `data`, `dataset`, `schema`, `tags`, `historian` | `data-reviewer` |
| `content`, `text`, `doc`, `spec`, `sop` | `content-reviewer` |
| `code`, `plc`, `scada`, `mes` | `code-reviewer` |
| `ui`, `ux`, `hmi`, `screen`, `frontend` | `ui-ux-reviewer` |
| `all` | all four in parallel + advisor |

## Behaviour

- Single kind → one `Task` call with the target as the prompt body.
- `all` → ONE message with four parallel `Task` blocks (data, content, code, ui). Then parse cross-talk pings, run Round-2 parallel batch if needed. Then dispatch `advisor` for final synthesis block.

All reviewers must: run live `WebSearch` / `WebFetch` for current best-practice references, emit `**Links**` + `**Cross-talk**` + `**Open questions**` envelope per `agents/_shared/council-protocol.md`.
