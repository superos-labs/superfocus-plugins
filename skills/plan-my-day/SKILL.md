---
name: plan-my-day
description: Build or repair the plan for one day on the Superfocus calendar - pick the daily highlight, time-block open tasks around existing events, move or clear blocks, and plan around sleep and the Stack. Use when the user says "plan my day", "plan tomorrow", "schedule my tasks", "my day is a mess", "what should I work on first and when", "block time for X", "move my 3pm" or "clear my afternoon". Not for just showing the calendar (morning-brief), capturing tasks from notes (capture-tasks), closing the day (end-of-day) or a week-level review (weekly-review).
---

# Plan my day

## When to use

The user wants a realistic plan for one day: what to do, in what order, and when. Also any single edit to that day's blocks.

## Which day

Default to today unless the user names the day. After 17:00 local, or when today has under two free hours left, plan tomorrow and say so. Never place anything in the past.

## Steps

1. Call `get_me` for the timezone, local date and time, sleep schedule and whether the Stack is on. Plan only between wake and sleep.
2. Call `get_goals` for priorities. Call `get_tasks` for open tasks with deadlines, estimates and `plannedFor`. Call `get_blocks` with `startDate` and `endDate` set to the day. Every block it returns is taken, recurring ones included.
3. Pick the daily highlight: the one task that matters most today. Order of preference: a task already planned for the day, then the nearest deadline, then the top task of the highest-priority goal. Put it in the first free deep-work slot.
4. Fill with fewer, longer blocks: two or three deep-work blocks with one concrete task each, then a short list of quick wins for the gaps. Plan at most four to six hours of task blocks. Never fill every free slot, leave a break after any meeting longer than an hour. If the plan does not fit, say what you left out and why.
5. A task the user wants on the day without a clock time gets `plannedFor` through `update_tasks` when the Stack is on, which projects it into free time. With the Stack off it needs a block.

## Before writing

Show the plan as a short list of times and tasks and ask for a yes. Do not call any write tool before the user agrees. No write tools listed: say edits are off for this connection (Superfocus > Settings > Integrations > MCP) and give the plan as text.

After a yes:

- `create_blocks` with `type` task and the task's `taskId` gives an existing task time. For new work call `create_tasks` with `startLocal` and `endLocal`, which creates the task and its block together. Use `type` protected only when the user asks to hold time for a goal.
- `update_blocks` with the `blockId` moves or resizes a block that already exists. `delete_blocks` clears one.
