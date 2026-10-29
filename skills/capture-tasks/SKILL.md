---
name: capture-tasks
description: Turn pasted notes, meeting minutes, emails, transcripts or a brain dump into Superfocus tasks under the right goals, with a duplicate check and one confirmation for three or more tasks. Use when the user pastes text and asks for action items, to-dos or next steps, says "add a task", "capture this", "remind me to", or lists things they need to do. Not for putting tasks on the calendar (plan-my-day) or listing existing tasks.
---

# Capture tasks

## When to use

The user has text, or a thought, and wants the actions saved as tasks.

## Steps

1. Call `get_me` for today's date and timezone, so "Friday" or "end of month" in the text resolve to real dates, and to see whether the Stack is on.
2. Extract the actions. One task per action, in plain words starting with a verb. Skip context that is not an action.
3. Call `get_goals` with `includeMilestones` true. Map each task to a goal, and to a milestone when the goal has an open one the task clearly serves. For ambiguous tasks pick the best fit and mark it with a question mark in the list. Ask one question for all of them together, never one per task.
4. Call `get_tasks` and skip anything that already exists. Say so, and use `update_tasks` only if the user wants that task changed.
5. Add an estimate or deadline only when the text says how long or due by when. A named day without a time goes to `plannedFor` when the Stack is on. With the Stack off, give the task `startLocal` and `endLocal` in the first free slot of that day, after `get_blocks` for that day.

Fast path: one or two tasks with an obvious goal need no list. Create them and report.

## Before writing

For more than two tasks, show the list (task, goal, deadline, day) and ask for a yes. No write tools listed: say edits are off for this connection (Superfocus > Settings > Integrations > MCP) and give the list as text.

After a yes, call `create_tasks` with each task's `goalId`, and `milestoneId`, `estimate`, `deadline`, `plannedFor` or `startLocal` plus `endLocal` where set.
