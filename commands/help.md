---
description: Quick reference — how to use the coptube plugin.
allowed-tools: 
---

Print this help verbatim to the user:

```
coptube — copper tube council + reviewers + harvester + company-intel + advisor

TRIGGER (type in any prompt)
  coptube <question>                full parallel council
  coptube:<selector> <question>     one agent
  coptube council <question>        same as bare coptube
  coptube advise <question>         advisor → council → decision
  coptube company <url|name>        scrape dossier
  coptube harvest <topic|all|url:…> fresh books/papers/blogs
  coptube review <kind> <target>    kind = data|content|code|ui|all

SLASH COMMANDS
  /coptube:ask <sel> <q>            dispatch single or council
  /coptube:council <q>              3-round parallel council
  /coptube:advise <q>               decision-ready output
  /coptube:review <kind> <target>   reviewer(s)
  /coptube:company <url>            dossier (add --engage/--compete/--buy)
  /coptube:harvest <topic|all>      refresh expert library
  /coptube:distribute               route _inbox/ to experts
  /coptube:list-updates [expert] [n] newest harvested notes
  /coptube:audit [--fix]            stale URLs / broken links / malformed
  /coptube:help                     this message

SELECTORS
  process | architect | qa | dev | manager | cyber | ops
  data | content | code-review | ui
  advisor | harvester | company
  council | review-all

HOW IT RUNS (superpowers-style parallel)
  Round 1  fan-out: one message, N Task calls concurrent
  Round 2  cross-talk: agents ping each other via @name, parallel resolve
  Round 3  advisor: synthesises SWOT + pros/cons + P0/P1/P2 actions

EVERY ANSWER INCLUDES
  · Protocol & era map (legacy → modern, format / datatype / periodicity)
  · SWOT anchored to your code + conversation
  · Pros / Cons with file:line evidence
  · Bottlenecks + hidden issues / loopholes
  · Live web links pulled at answer time
  · Cross-talk pings + open questions

EXAMPLES
  coptube how do I scope a 30 kt/yr pilger line bid?
  coptube:cyber is Basic256Sha256 still acceptable in 2026?
  coptube review all src/plc/pass_schedule.st
  coptube company https://www.hailiang.com --compete
  coptube harvest all
  coptube advise do we pick SMS or Danieli?

DOCS
  README.md                         full guide + install
  agents/_shared/council-protocol.md shared rules
  skills/coptube/references/        knowledge base
```

If user asked a specific question ("how do I do X"), after printing the message above, also answer it by dispatching the best-fit subagent via Task.
