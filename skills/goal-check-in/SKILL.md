---
name: goal-check-in
description: Report progress, blockers and the next milestone for one goal or every goal in the current Superfocus season, with focus hours per goal, and apply goal or milestone changes after confirmation. Use when the user asks how a goal is going, whether they are on track, what is blocking a goal, what milestone comes next, or wants to create, complete, rename or re-deadline a goal or milestone. Not for planning a day (plan-my-day) or reviewing the week (weekly-review).
---

# Goal check-in

## When to use

The user wants to see where they stand on one goal or all of them, and what to do next. Also goal and milestone setup.

## Steps

1. Call `get_me` for today's date and the current season. Cover only this season's goals unless the user names another.
2. Call `get_goals` with `includeMilestones` true and `includeTasks` true. Call `get_stats` for planned against spent hours per goal for the period the user names (week, month or quarter, default week). Use `get_focus` with `days` only when the user asks about specific days.
3. For each goal, report:
   - Progress per milestone: done, in progress or overdue, with its deadline and how many of its tasks are open.
   - Hours in that period against the goal's priority.
   - Blockers, only when checkable: the next milestone has no open tasks, the goal got no time in the period, or a milestone deadline has passed.
   - Next milestone: the nearest unfinished one and the first task to move it.
4. Keep it to a few lines per goal. If the user asked about one goal, cover only that goal.

## Before writing

Only change something when the user asks. Show the proposed change, for example "mark milestone X as reached" or "move its deadline to 2026-11-15", and ask for a yes. Marking a milestone reached also completes its tasks and removes their calendar blocks, so say that before asking. No write tools listed: say edits are off for this connection (Superfocus > Settings > Integrations > MCP).

After a yes: `update_goals` and `update_milestones` change existing ones, `create_goals` adds a goal, `create_milestones` adds a milestone under its `goalId`.
