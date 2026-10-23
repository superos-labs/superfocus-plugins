---
name: capture-tasks
description: Turn pasted notes, meeting text or a brain dump into tasks under the right goals. Use when the user pastes text and asks for action items, or says to add or capture tasks.
---

# Capture tasks

## When to use

The user pastes notes, a transcript, an email or a list and wants the actions saved as tasks.

## Steps

1. Extract the actions. One task per action, in plain words starting with a verb. Skip context that is not an action.
2. Call `get_goals` to see the user's goals and their ids. Map each task to a goal. When a task could fit more than one goal, or none, ask the user instead of guessing.
3. Call `get_tasks` to avoid duplicating a task that already exists. If one exists, say so and use `update_tasks` only if the user wants a change.
4. Add an estimate or deadline only when the text gives one. If the text names a day for a task, note it for `plannedFor`.
5. Call `get_me` before using `plannedFor` to check whether the Stack is on.

## Before writing

Show the list: task, goal, deadline, day. Ask for a yes. Do not call `create_tasks` before the user agrees. If the write tools are not listed, tell the user edits are off for this connection and point them to Settings > Integrations > MCP in Superfocus. You can still give the list as text.

After a yes, call `create_tasks` with the `goalId` of each task. When the Stack is on and a day was given without a time, set `plannedFor` as `YYYY-MM-DD`. When the Stack is off, give the task a start and end in the first free slot of that day, in local time `YYYY-MM-DD HH:mm`, after checking `get_blocks` for that day. Use only ids returned by the read tools.

Finish by listing what you created.
