---
description: Ask the advisor for a decision. Advisor auto-runs the council first, then synthesises. Usage:/coptube:advise <question>
argument-hint: <question>
allowed-tools: Task
---

Dispatch `advisor` with `$ARGUMENTS`. Advisor will:

1. If no prior council transcript in the conversation, fan out the full council via parallel `Task` calls.
2. Collect Round-1 + Round-2 cross-talk replies.
3. Write the `⚖️ Council consensus` block — decision-ready, with prioritized actions, risk register, budget/schedule snapshot, decisions the user still owes, and the "if I'm wrong" assumption.

Use when the user wants a decision, not a discussion.
