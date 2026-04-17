---
description: Run full parallel coptube council on a question. Usage:/coptube:council <question>
argument-hint: <question>
allowed-tools: Task
---

Full council. Three-round parallel orchestration.

### Round 1 — parallel fan-out

ONE message containing SEVEN `Task` blocks:
- `process-expert`
- `software-architect`
- `qa-tester`
- `developer`
- `manager`
- `cybersecurity-expert`
- `operations-expert`

If `$ARGUMENTS` mentions code / schema / doc / UI, add in parallel:
- `code-reviewer` / `data-reviewer` / `content-reviewer` / `ui-ux-reviewer`

### Round 2 — cross-talk

Parse every returned section for `> @<agent>:` lines. Group questions by target agent. Fire ONE message with parallel `Task` calls — one per target — passing the grouped question list.

### Round 3 — synthesis

Dispatch `advisor` via `Task` with the full transcript of Rounds 1–2 concatenated into the prompt. Advisor writes the `⚖️ Council consensus` block with prioritized actions, risk register, and decisions-owed.

### Output

Stitch to user: every Round-1 section, every Round-2 reply, then advisor's consensus. Preserve all `**Links**` blocks.

Protocol reference: `agents/_shared/council-protocol.md`.
