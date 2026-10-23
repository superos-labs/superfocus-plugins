---
name: weekly-review
description: Run the user's weekly review. Use when they ask how their week went, want a weekly retro, ask where their time went, or want to plan next week from what happened.
---

# Weekly review

## When to use

The user wants to look back at the week and decide what to change.

## Steps

1. Call `get_me` for the timezone and today's date.
2. Call `get_reviews` with `period` weekly for the latest weekly review. Call `get_focus` with `days` 7 for the focus score per day and hours per goal.
3. Call `get_goals` with `includeMilestones` true for goal priorities, notes and milestone deadlines.
4. Write the review:
   - Wins: what moved, with numbers where you have them.
   - Misses: what slipped or got no time.
   - Hours per goal against intent: compare time spent with each goal's priority. Core goals should get the most time.
   - One suggestion per goal, concrete and small.
5. Offer to plan next week. If the user says yes, call `get_tasks` and `get_blocks` for next week's dates and propose blocks for the goals that were short on time. If `propose_changes` is listed, propose them with it so the user can adjust and keep them from the planner card.

## Before writing

Reading and summarizing needs no confirmation. Before any write, show the proposed blocks and ask for a yes. Do not call `create_blocks` or `update_blocks` before the user agrees. If the write tools are not listed, tell the user edits are off for this connection and point them to Settings > Integrations > MCP in Superfocus.

Keep the review short. Say plainly when there is not enough data for a goal.
