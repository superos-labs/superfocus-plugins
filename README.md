# Superfocus

Superfocus is a planning app built around seasons. A Season holds Goals, Goals hold Milestones and Tasks, and Tasks get time on your calendar as Blocks. This plugin connects your Superfocus account to your AI assistant through the Superfocus MCP server at `https://mcp.superfocus.me/mcp`, so the assistant can read your plan and, if you allow it, change it.

The same repository works as a Claude plugin, an OpenAI plugin package and a Gemini CLI extension.

## What you get

Six skills:

- `morning-brief`: five lines on today, meetings, the block worth protecting, free stretches and clashes. Read-only.
- `plan-my-day`: picks the daily highlight, time-blocks open tasks around existing events with fewer, longer blocks, moves or clears blocks after you agree.
- `end-of-day`: what got done against the plan, carries unfinished work to tomorrow, saves a short wins note.
- `weekly-review`: wins and misses with counts, hours per goal against your intent, one suggestion per goal, optional journal note and time next week.
- `capture-tasks`: turns pasted notes or meeting text into tasks mapped to your goals and milestones.
- `goal-check-in`: progress per milestone, hours per goal, checkable blockers and the next milestone; creates or updates goals and milestones after you agree.

The server also exposes read tools (profile, goals, tasks, blocks, recurring items, reviews, focus score, journal, activity, focus sessions, latest assessment, meeting notes, screen time, stats) and, only when your grant allows edits, write tools for blocks, tasks, goals, milestones, sleep schedule, journal notes and notes for the Superfocus coach.

## Install

You need a Superfocus account. Sign-in uses OAuth 2.1 with PKCE, and you choose whether to allow edits when you connect.

Claude (Claude Code):

```
/plugin marketplace add superos-labs/superfocus-plugins
/plugin install superfocus@superfocus-plugins
```

Or upload this folder as a zip in Customize > Plugins > Add > Upload plugin, then connect Superfocus from the plugin's Connectors tab.

OpenAI (ChatGPT / Codex): add this repository as a plugin source and connect Superfocus when prompted. The package uses `plugin.json` and `mcp.json` at the repository root.

Gemini CLI:

```
gemini extensions install https://github.com/superos-labs/superfocus-plugins
```

## Edits

Read access is always on. If the write tools are missing, edits are off for your connection. Change this in Superfocus under Settings > Integrations > MCP. The skills always show proposed changes and ask for a yes before writing.

## Privacy Policy

When you use this plugin, your assistant sends requests to `mcp.superfocus.me` and receives the parts of your Superfocus data it asks for, such as goals, tasks, calendar blocks and reviews. Anything you ask it to write is saved to your Superfocus account. The plugin itself stores nothing and contains no code. How Superfocus handles your data is described at https://superfocus.me/privacy. Terms: https://superfocus.me/terms.

## Support

help@superfocus.me, https://superfocus.me/mcp

## License

MIT, see `LICENSE`. Copyright 2026 SuperOS Labs.
