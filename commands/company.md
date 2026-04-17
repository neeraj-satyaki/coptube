---
description: Scrape a company (site + blog + news + filings + social + patents) and write a dossier. Usage:/coptube:company <url or name>
argument-hint: <url-or-name> [--engage|--compete|--buy]
allowed-tools: Task
---

Dispatch `company-intel` with `$ARGUMENTS`. Agent follows its own workflow: verify identity → deep site scrape → parallel outside-in web search (news, press, filings, LinkedIn, YouTube, patents, sanctions) → triangulate vs `industry-research.md` → write `references/companies/<slug>/dossier.md` → register in INDEX.

If `$ARGUMENTS` contains `--engage`, `--compete`, or `--buy`, after dossier is written, chain to `advisor` via another `Task` with the dossier path — advisor fans out the council for the strategic question.

Return to user: dossier path + TL;DR + top 3 findings + red flags + next-move suggestion.
