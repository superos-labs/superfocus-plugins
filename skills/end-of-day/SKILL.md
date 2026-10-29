---
name: end-of-day
description: Close the day in Superfocus - what got done against the plan, what to carry over to tomorrow, and a short wins note for the journal. Use when the user says "wrap up my day", "what did I get done today", "close the day", "move what I didn't finish to tomorrow", "today's wins" or "log my day". Not for planning tomorrow in full (plan-my-day) or the week (weekly-review).
---

# End of day

## When to use

The day is ending. The user wants a quick account of it and a clean start tomorrow.

## Steps

1. Call `get_me` for the timezone and local date.
2. Call `get_blocks` with `startDate` and `endDate` set to today. Split task blocks into done and not done from their completion state. Call `get_tasks` with `includeCompleted` true for tasks completed today and open tasks with `plannedFor` today.
3. Report in a few lines: what got done, what did not, and the one thing that mattered most.
4. For each unfinished task block or planned task, propose one of: carry it to tomorrow, drop it, or mark it done if the user says it happened. Default is carry over.
5. Offer a two-line wins note for the journal, in the user's voice.

## Before writing

Show the carry-over list and the note and ask for a yes. No write tools listed: say edits are off for this connection (Superfocus > Settings > Integrations > MCP) and give the summary as text.

After a yes:

- Carry over a block: `update_blocks` with the `blockId` and tomorrow's `startLocal` and `endLocal` in a free slot (check tomorrow with `get_blocks` first). If the Stack is on and the user does not care about the time, set `plannedFor` tomorrow on the task with `update_tasks` and `delete_blocks` on today's block instead.
- Carry over a planned task with no block: `update_tasks` with `plannedFor` tomorrow.
- Done after all: `update_tasks` with `completed` true, which closes the task. Use `update_blocks` with `completed` true only when the user wants the block marked and the task kept open.
- Drop: `delete_blocks` for the block, or `update_tasks` with `plannedFor` null for a planned task.
- Note: `save_journal_note`.
