---
description: Ask coptube. Single expert/reviewer, or full parallel council. Usage:/coptube:ask <selector> <question>
argument-hint: <selector> <question>
allowed-tools: Task, Read, Grep, Glob, WebSearch, WebFetch
---

Parse `$ARGUMENTS`. First token = selector. Rest = question.

## Selector map

| Aliases | Subagent |
|---|---|
| `process`, `dr-p`, `metallurgy` | `process-expert` |
| `architect`, `arch`, `software` | `software-architect` |
| `qa`, `quinn`, `test`, `validation` | `qa-tester` |
| `dev`, `developer`, `code`, `plc` | `developer` |
| `manager`, `mgr`, `pm`, `capex` | `manager` |
| `cyber`, `security`, `ot-sec` | `cybersecurity-expert` |
| `ops`, `operations`, `reliability` | `operations-expert` |
| `data` | `data-reviewer` |
| `content`, `text`, `doc` | `content-reviewer` |
| `code-review` | `code-reviewer` |
| `ui`, `ux`, `hmi`, `screen` | `ui-ux-reviewer` |
| `company`, `intel` | `company-intel` |
| `harvester`, `books`, `blogs` | `knowledge-harvester` |
| `advisor`, `advise`, `strategy` | `advisor` |
| `council`, `all`, `seven` | full parallel council |
| `review-all` | 4 reviewers parallel + advisor |

## Behaviour (mandatory)

1. **Single selector** → dispatch one `Task` call with that `subagent_type` and the user's question. Wait for return, relay.

2. **`council`** → **Round 1:** ONE message with SEVEN parallel `Task` blocks (`process-expert`, `software-architect`, `qa-tester`, `developer`, `manager`, `cybersecurity-expert`, `operations-expert`). Add reviewer subagents to the same parallel batch when the question obviously needs them (reviewing code, docs, data, or UI).
    **Round 2:** Parse every returned section for `> @<agent>:` lines. Group by target. Fire ONE message with parallel `Task` calls, one per pinged agent, containing the question list addressed to that agent.
    **Round 3:** Dispatch `advisor` via `Task`, passing the concatenated transcript of Rounds 1–2. Advisor writes the `⚖️ Council consensus`.
    Return to user: all per-expert sections + Round-2 replies + final consensus.

3. **`review-all`** → Round 1 parallel: `data-reviewer`, `content-reviewer`, `code-reviewer`, `ui-ux-reviewer`. Round 2 cross-talk if emitted. Round 3 `advisor`.

4. **Unknown selector** → show the table above, ask which. Do not guess.

## Critical rules

- Parallel means one message, multiple `Task` tool-use blocks. Never serialize Round-1 calls.
- Do not summarize away individual expert voices; preserve them, then let advisor reconcile.
- If any sub-agent emits `**Links**` block, preserve those URLs in the final output.
- If any sub-agent emits `**Cross-talk**` pings, Round 2 is mandatory — do not skip.
