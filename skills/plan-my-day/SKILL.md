---
name: plan-my-day
description: Plan the user's day on their calendar. Use when they ask to plan today or another day, schedule their tasks, fix a messy day, or decide what to work on first.
---

# Plan my day

## When to use

The user wants a realistic plan for a day: what to do, in what order, and when.

## Steps

1. Call `get_me` for the timezone, local date and time, sleep schedule and whether the Stack is on. Plan around the sleep schedule and never in the past.
2. Call `get_tasks` for open tasks. Note deadlines, estimates and `plannedFor` dates. Call `get_blocks` with `startDate` and `endDate` set to the day to see what is already booked.
3. Pick the daily highlight: the one task that matters most today, usually the one tied to a core goal or a near deadline. Put it first.
4. Propose a plan with fewer, longer blocks. Group small tasks into one block. Keep every existing event and protected block where it is. Leave gaps for breaks. If the plan does not fit, say what you left out and why.
5. If the Stack is on, tasks the user only wants on a day without a time can be set with `plannedFor` instead of a block.

## Before writing

Show the proposed plan as a short list of times and tasks, and ask for a yes. Do not call any write tool before the user agrees. If the write tools (`create_blocks`, `update_blocks`) are not listed, tell the user edits are off for this connection and point them to Settings > Integrations > MCP in Superfocus. You can still give the plan as text.

After a yes:

- Call `create_blocks` with `type` task and the task's `taskId` to give an existing task time. For new work call `create_tasks` with `startLocal` and `endLocal` so the task and its block are created together. Use `type` protected only when the user asks to hold time for a goal. Times are local, `YYYY-MM-DD HH:mm`.
- Call `update_blocks` with the `blockId` to move or resize a block that already exists. Moving never creates a second block.
- Use only ids returned by the read tools. Never invent an id.

Finish by saying exactly what you created or changed.
