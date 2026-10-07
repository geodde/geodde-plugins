# Geodde plugins

Write pages that get your brand cited by AI assistants, from your [Geodde](https://geodde.com) content roadmap.

The `geodde` plugin adds two things:

- **The Geodde connector** (`https://app.geodde.com/mcp`) — your roadmap, topics, prompts, brand facts and pages. You sign in with your Geodde account and choose which sites it can use.
- **The `write-geodde-page` skill** — picks the top roadmap topic, claims it, reads the page brief, researches, writes every section and sends the draft back to Geodde for review. Nothing is published until someone approves it in Geodde.

## Install

**Claude Code**

```
/plugin marketplace add geodde/geodde-plugins
/plugin install geodde@geodde
```

**Codex**

```
codex plugin marketplace add geodde/geodde-plugins
```

Then install `geodde` from `/plugins`.

**claude.ai, ChatGPT, or one skill on its own**

Download the skill from the Skills page in Geodde and upload it (claude.ai: Customize → Skills; ChatGPT: Skills → Create → Upload). Add the connector separately — the MCP Access page in Geodde has the steps.

## Layout

One plugin, readable by both Claude Code and the Agent Plugins format Codex and ChatGPT use:

```
.claude-plugin/marketplace.json     Claude Code marketplace
.agents/plugins/marketplace.json    Codex marketplace
geodde/
  .claude-plugin/plugin.json        Claude Code manifest
  .mcp.json                         Claude Code connector
  plugin.json                       Agent Plugins manifest
  mcp.json                          Agent Plugins connector
  skills/write-geodde-page/SKILL.md the skill (open Agent Skills format)
```

This repo is published from `plugins/` in Geodde's app repository — change it there.
