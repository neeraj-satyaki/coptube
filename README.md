# coptube — Claude Code plugin

Council of **7 experts + 4 reviewers + advisor + knowledge harvester + company-intel scraper** for copper / brass / cupronickel tube manufacturing and plant automation. Runs in parallel (superpowers-style). Agents cross-talk, pull live web sources, advisor synthesises.

## Trigger — type the skill name in any prompt

Any message mentioning `coptube` activates the plugin. Free-form OR structured:

```
coptube how should I architect Level 2 for a 30 kt/yr pilger line?
coptube:cyber review my IEC 62443 zone diagram
coptube council should we pilot Ignition Perspective on the 3rd mill?
coptube company https://www.hailiang.com
coptube harvest all
coptube review all src/plc/pass_schedule.st
coptube advise do we sign SMS or Danieli for the ACR line?
```

Slash commands also available (see below).

## Agents

### 7 experts
| Selector aliases | Agent | Lens |
|---|---|---|
| `process` / `dr-p` / `metallurgy` | `process-expert` | 🏭 Dr. P — PhD process & automation |
| `architect` / `arch` / `software` | `software-architect` | 🏗️ Arch — ISA-95 / OPC UA / MES |
| `qa` / `quinn` / `test` | `qa-tester` | 🧪 Quinn — FAT / SAT / HAT |
| `dev` / `developer` / `code` / `plc` | `developer` | 💻 Dev — PLC / SCADA / MES code |
| `manager` / `mgr` / `pm` / `capex` | `manager` | 📋 Mgr — cost / schedule / vendors |
| `cyber` / `security` / `ot-sec` | `cybersecurity-expert` | 🛡️ Cyber — IEC 62443 / OT security |
| `ops` / `operations` / `reliability` | `operations-expert` | 🔧 Ops — OEE / PdM / reliability |

### 4 reviewers
| Selector aliases | Agent | Focus |
|---|---|---|
| `data` | `data-reviewer` | 📊 Schemas, tags, historian, datasets — bottlenecks + hidden pain points |
| `content` / `text` / `doc` | `content-reviewer` | 📝 Specs, SOPs, manuals, harvester notes — clarity + compliance |
| `code-review` | `code-reviewer` | 💻 PLC / SCADA / web code — correctness, security, determinism, CVEs |
| `ui` / `ux` / `hmi` | `ui-ux-reviewer` | 🎨 HMI + web UI — ISA-101, ISA-18.2, WCAG 2.2, Core Web Vitals |

### Meta agents
| Selector aliases | Agent | Role |
|---|---|---|
| `advisor` / `advise` / `strategy` | `advisor` | ⚖️ Synthesises council into decision-ready consensus |
| `harvester` / `books` / `blogs` | `knowledge-harvester` | Finds books (PDF/EPUB), papers, standards, blogs — routes to expert folders |
| `company` / `intel` | `company-intel` | Scrapes company site + blog + news + filings + patents — writes dossier |

## How parallel execution works (superpowers-style)

1. **Round 1 — parallel fan-out.** Orchestrator sends ONE message with multiple `Task` tool-use blocks. All agents run concurrently.
2. **Round 2 — cross-talk.** Each agent can emit `> @<agent>: <question>` pings. Orchestrator groups by target and fires another parallel `Task` batch.
3. **Round 3 — advisor synthesis.** Advisor reads full transcript, writes the final `⚖️ Council consensus`.

Every non-trivial answer also: runs live `WebSearch` + `WebFetch`, cites URLs in `**Links**` block, lists `**Open questions**`.

Full protocol: `agents/_shared/council-protocol.md`.

## Slash commands

| Command | What it does |
|---|---|
| `/coptube:ask <selector> <q>` | Single agent, or `council` for full parallel |
| `/coptube:council <q>` | Explicit full council with 3-round orchestration |
| `/coptube:advise <q>` | Advisor (auto-runs council first) |
| `/coptube:review <kind> <target>` | `data` / `content` / `code` / `ui` / `all` |
| `/coptube:company <url-or-name> [--engage/--compete/--buy]` | Company dossier |
| `/coptube:harvest <topic \| all \| expert:x \| url:…>` | Find + file fresh sources |
| `/coptube:distribute` | Route `_inbox/` notes to right expert |
| `/coptube:list-updates [expert] [count]` | Show newest harvested notes |
| `/coptube:audit [--fix]` | Check stale URLs, broken links, malformed front-matter |

## Install

### Local (single machine)

```bash
# Windows (bash)
mkdir -p "$HOME/.claude/plugins/coptube"
cp -r /path/to/coptube/* "$HOME/.claude/plugins/coptube/"

# macOS / Linux
mkdir -p ~/.claude/plugins/coptube
cp -r /path/to/coptube/* ~/.claude/plugins/coptube/
```

Or symlink (stay editable in place):

```bash
ln -s "/g/My Drive/D-backup/Projects/Skills/Copper-industry/coptube" "$HOME/.claude/plugins/coptube"
```

Restart Claude Code. Verify: `/plugin` — `coptube` should appear.

### Marketplace (team distribution)

1. Push folder to git repo.
2. Add `.claude-plugin/marketplace.json` at repo root listing the plugin.
3. Users:
   ```
   /plugin marketplace add <you>/coptube
   /plugin install coptube@<you>/coptube
   ```

### Zip

Re-zip the folder as `coptube-plugin.zip`, ship it, extract into `~/.claude/plugins/`.

## Directory layout

```
coptube/
├── .claude-plugin/plugin.json
├── agents/
│   ├── _shared/council-protocol.md     # cross-talk + parallel + web-search rules
│   ├── process-expert.md               # 🏭 Dr. P
│   ├── software-architect.md           # 🏗️ Arch
│   ├── qa-tester.md                    # 🧪 Quinn
│   ├── developer.md                    # 💻 Dev
│   ├── manager.md                      # 📋 Mgr
│   ├── cybersecurity-expert.md         # 🛡️ Cyber
│   ├── operations-expert.md            # 🔧 Ops
│   ├── data-reviewer.md                # 📊
│   ├── content-reviewer.md             # 📝
│   ├── code-reviewer.md                # 💻
│   ├── ui-ux-reviewer.md               # 🎨
│   ├── advisor.md                      # ⚖️
│   ├── knowledge-harvester.md
│   └── company-intel.md
├── commands/
│   ├── ask.md · council.md · advise.md
│   ├── review.md · company.md
│   ├── harvest.md · distribute.md · list-updates.md · audit.md
├── skills/coptube/
│   ├── SKILL.md · README.md
│   └── references/
│       ├── 01..07-*.md                 # persona files
│       ├── industry-research.md
│       ├── deep-dives/*.md             # 9 deep-dives
│       ├── updates/                    # harvester output
│       │   ├── INDEX.md · _inbox/
│       │   └── <expert>/…
│       └── companies/                  # company-intel output
└── README.md
```

## Typical sessions

### Full council
```
> coptube council how do I scope a 30 kt/yr pilger line bid?

# Round 1: 7 experts in parallel, each cites live sources
# Round 2: cross-talk pings resolved in parallel
# Round 3: advisor writes consensus with P0/P1/P2 actions
```

### Just one expert
```
> coptube:cyber is OPC UA SecurityPolicy Basic256Sha256 still acceptable in 2026?
# Cyber answers alone, pulls live CVEs + IEC 62443 revision checks
```

### Review a PR
```
> coptube review all path/to/diff
# data-reviewer + content-reviewer + code-reviewer + ui-ux-reviewer in parallel
# advisor consolidates into prioritized fix list
```

### Research a competitor
```
> coptube company https://www.hailiang.com --compete
# company-intel scrapes, advisor routes to council for strategic angle
```

### Refresh expert knowledge
```
> coptube harvest all
# harvester fills one gap per expert from books / papers / standards / blogs
```

## Harvester rules (short)

- Open Access / standards / CC-licensed preferred.
- Quotes ≤ 25 words with source.
- No piracy sites. Archive.org, DOAB, OpenStax, publisher OA portals allowed.
- Unverified URLs never saved.
- Deduplicates by DOI / URL.
- Per-expert front-matter (routes, relevance, license).

Full rules: `agents/knowledge-harvester.md`.

## Extending

- New expert → copy `agents/*.md`, edit `description`, add `references/08-<expert>.md`, add routing in SKILL.md + ask.md + `updates/INDEX.md`.
- New reviewer → copy a reviewer file, aim at a new artefact type.
- New command → `commands/<name>.md` with YAML front-matter (`description`, `allowed-tools`).
- New deep-dive → drop in `skills/coptube/references/deep-dives/`, add row in SKILL.md table.

## License

Plugin scaffolding: MIT. Reference notes carry source license in `license_note` — respect it.
