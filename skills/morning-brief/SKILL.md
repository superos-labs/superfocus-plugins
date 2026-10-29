---
name: morning-brief
description: A short read-only brief of the user's day from Superfocus - meetings in order, the one block that moves their core goal, free stretches, and any overlap or gap that needs a decision. Use when the user asks "what's on today", "what's on tomorrow", "what does Friday look like", "brief me", "what's next", "what's on my calendar" or "any clashes today". Not for changing the plan (plan-my-day).
---

# Morning brief

## When to use

The user wants to know what a day holds, in a few lines, without changing anything. Default today, or the day they name.

## Steps

1. Call `get_me` for the timezone, local date and time.
2. Call `get_blocks` with `startDate` and `endDate` set to that day. Call `get_goals` to know which goal is core. Call `get_tasks` for open tasks with a deadline on or before that day.
3. Write five lines or fewer:
   - Meetings and events in order, with times. Skip the ones already over when asked after noon.
   - The one task block that moves the core goal and is worth protecting.
   - Free stretches of an hour or more.
   - Any overlap, or a gap where a deadline task has no time.
4. If a clash has an obvious fix, name it in one line and offer to apply it with the plan-my-day steps. Do not propose tasks or new blocks otherwise.

Nothing is written. Answer only with what the day already holds.
