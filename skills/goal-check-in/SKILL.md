---
name: goal-check-in
description: Check progress on the user's goals. Use when they ask how a goal is going, what is blocking them, what milestone is next, or want to update or complete a goal or milestone.
---

# Goal check-in

## When to use

The user wants to see where they stand on one goal or all of them, and what to do next.

## Steps

1. Call `get_me` for today's date and the current season.
2. Call `get_goals` with `includeMilestones` true and `includeTasks` true.
3. For each goal, report:
   - Progress per milestone: done, in progress or overdue, with its deadline and how many of its tasks are open.
   - Blockers: overdue milestones, goals with no open tasks, tasks with no estimate or deadline that stall the next milestone.
   - Next milestone: the nearest unfinished one and the first task to move it.
4. Keep it to a few lines per goal. If the user asked about one goal, cover only that goal.

## Before writing

Only change something when the user asks. Show the proposed change, for example "mark milestone X as reached" or "move its deadline to 2026-11-15", and ask for a yes. Marking a milestone reached also completes its tasks and removes their calendar blocks, so say that before asking. Do not call `update_milestones` or `update_goals` before the user agrees. If the write tools are not listed, tell the user edits are off for this connection and point them to Settings > Integrations > MCP in Superfocus.

Use only goal and milestone ids returned by `get_goals`. Finish by saying what you changed.
