---
name: weekly-review
description: Look back at the past week in Superfocus - focus hours per goal against priority, tasks and milestones completed, wins, misses and one small change per goal, then optionally hold time next week for goals that fell short. Use when the user asks how their week went, wants a weekly review or retro, asks where their time went this week or what they got done, or wants a Friday wrap-up or Sunday reset. Not for a single day (end-of-day), one goal's status (goal-check-in) or planning a specific day (plan-my-day).
---

# Weekly review

## When to use

The user wants to understand the week that just happened and carry one lesson into the next one.

## Which week

Monday or Tuesday means last calendar week. Any other day means this week so far. Pass explicit dates to every tool.

## Steps

1. Call `get_me` for the timezone and today's date, then work out the Monday of the window yourself.
2. Call `get_focus` with `days` covering the window for the focus score per day and hours per goal. Call `get_stats` for planned against spent hours per goal this week.
3. Call `get_goals` with `includeMilestones` true for priorities and milestone deadlines. Call `get_tasks` with `includeCompleted` true and keep only tasks completed inside the window.
4. Call `get_reviews` with `period` weekly. If a review already covers this window, build on it instead of restarting. Call `get_journal` for notes from the week.
5. Write the review:
   - Wins: tasks and milestones completed, with counts.
   - Misses: what slipped or got no time.
   - Hours per goal against intent: compare spent hours with each goal's priority. Core goals should get the most time.
   - One suggestion per goal, concrete and small.
6. Offer to save the review as a journal note with `save_journal_note`, written in the user's voice. If one pattern repeats across weeks, offer to store it with `remember` so the Superfocus coach keeps it.
7. Offer to hold time next week for the goals that fell short. On a yes, propose `create_blocks` with `type` protected and the goal's `goalId`, and follow the plan-my-day skill for the days the user picks.

## Before writing

Reading and summarizing needs no confirmation. Before any write, show what you will save or book and ask for a yes. No write tools listed: say edits are off for this connection (Superfocus > Settings > Integrations > MCP) and deliver the review as text.

Keep the review short. Say plainly when there is not enough data for a goal.
