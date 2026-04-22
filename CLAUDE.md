# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A Claude Code plugin (`coptube`) — a standing council of 7 domain experts + 4 reviewers + 3 meta-agents for copper/brass/cupronickel tube manufacturing and plant automation. No build step, no test runner — the artefacts are Markdown prompt files read by the Claude Code plugin runtime.

## Triggering the plugin

Any message containing `coptube` activates the plugin. Routing is parsed before dispatch:

| Pattern | Dispatches to |
|---|---|
| `coptube <question>` | Full council (7 experts parallel → cross-talk → advisor) |
| `coptube:<selector> <question>` | Single agent |
| `coptube council <question>` | Same as bare `coptube` |
| `coptube review all <target>` | 4 reviewers parallel + advisor |
| `coptube harvest <topic\|all\|url:…>` | `knowledge-harvester` |
| `coptube company <url-or-name>` | `company-intel` |
| `coptube advise <question>` | `advisor` (auto-runs council first) |
| `coptube distribute` | `knowledge-harvester` in route mode |
| `coptube audit` | `knowledge-harvester` in audit mode |
| `coptube list-updates [expert] [count]` | list-updates command logic |

Slash-command equivalents live in `commands/` (`/coptube:ask`, `/coptube:council`, etc.).

## Architecture

```
coptube/
├── .claude-plugin/
│   ├── plugin.json          # plugin manifest (name, version, homepage)
│   └── marketplace.json     # marketplace distribution metadata
├── agents/
│   ├── _shared/
│   │   └── council-protocol.md   # binding rules for ALL agents (parallel dispatch,
│   │                             #   cross-talk, web-search duty, SWOT/pros-cons,
│   │                             #   output envelope, protocol-era lens)
│   └── <agent>.md           # 14 agent definitions (7 experts, 4 reviewers, 3 meta)
├── commands/
│   └── <command>.md         # slash-command handlers (YAML front-matter + instructions)
└── skills/coptube/
    ├── SKILL.md             # master skill file — trigger phrases, routing table,
    │                        #   selector map, answer shape, style rules
    └── references/
        ├── 01..07-*.md      # persona files (one per expert — read before answering)
        ├── industry-research.md   # OEM/vendor/producer/standard index with URLs
        ├── deep-dives/      # 10 deep-dive reference files (load on topic match)
        └── updates/         # harvester output
            ├── INDEX.md     # routing map + front-matter spec
            ├── _inbox/      # unrouted items awaiting /coptube:distribute
            └── <expert>/    # newest notes per expert (read newest-first per answer)
```

### Three-round parallel execution

1. **Round 1** — orchestrator sends ONE message with multiple `Task` blocks (one per expert). All run concurrently.
2. **Round 2** — agents emit `> @<agent>: <question>` cross-talk lines. Orchestrator groups by target and fires another parallel `Task` batch.
3. **Round 3** — `advisor` reads full Round 1+2 transcript, writes `⚖️ Council consensus`.

Never serialize Round-1 calls. Protocol is in `agents/_shared/council-protocol.md`.

## How agents work

Every agent reads `agents/_shared/council-protocol.md` first (binding for all). For answers, each also reads its persona file (`references/01..07-*.md`) and any relevant deep-dive files — never relies on memory alone.

**Output envelope** (mandatory per section):
- Protocol & era (tier, format, datatype, periodicity, loophole)
- SWOT + Pros/Cons anchored to specific evidence
- Bottlenecks, Hidden issues, Links, Cross-talk, Open questions

## Knowledge harvester

Adds research notes to `skills/coptube/references/updates/<expert>/`. Naming: `YYYY-MM-DD__<slug>__<source-domain>.md`. Every file requires front-matter: `harvested_at`, `source_url`, `source_type`, `title`, `authors`, `expert_routes`, `relevance`, `license_note`.

Unrouted items land in `_inbox/`; run `coptube distribute` to route them.

## Extending

- **New expert** → copy an `agents/*.md`, add `references/08-<expert>.md`, add routing in `SKILL.md` + `commands/ask.md` + `updates/INDEX.md`.
- **New reviewer** → copy a reviewer agent file, target a new artefact type.
- **New slash command** → `commands/<name>.md` with YAML front-matter (`description`, `allowed-tools`).
- **New deep-dive** → drop in `skills/coptube/references/deep-dives/`, add row in `SKILL.md` deep-dive table.
