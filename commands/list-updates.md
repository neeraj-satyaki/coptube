---
description: Show freshest harvested notes per expert. Usage:/coptube:list-updates [expert] [count]
argument-hint: [expert] [count=5]
allowed-tools: Bash, Read, Glob
---

## Task

1. Parse `$ARGUMENTS`: optional expert name, optional count (default 5).
2. If expert given → list newest `count` files in `skills/coptube/references/updates/<expert>/`.
3. Else → for each of the 7 experts, list newest `count` files.
4. Show as a table: date · expert · title · source_type · relevance (read front-matter to extract).
5. End with counts per expert and `_inbox/` size.

Use `Glob` with pattern `skills/coptube/references/updates/*/*.md`, sort by mtime desc, then `Read` each matched file's front-matter only (first ~15 lines).
