# ORTEX for Claude: plugin

ORTEX short-selling and market data inside Claude, plus skills that show Claude how to
read it.

This repo is a **Claude plugin marketplace**. Installing the plugin gives you:

- **The ORTEX connector:** 34 read-only tools for short interest, cost to borrow, days to
  cover, availability, options analytics, stock scores, US government (Congress) trades,
  fundamentals, prices and ETF holdings, through the remote MCP server at `mcp.ortex.com`.
- **Two skills:** `ortex-short-analysis` (how to read short-selling data together and
  present a verdict with its evidence) and `get-started` (what you can ask).

Everything is read-only. ORTEX never places trades or moves money, and it does not give
personal investment advice. The data you can reach is what your ORTEX plan includes.

## Install (Claude Code)

```
/plugin marketplace add ortex-financial/ortex-claude-plugin
/plugin install ortex
```

Then authorize ORTEX when prompted: sign in to your ORTEX account and click **Authorize**.
Which datasets you can read depends on your ORTEX plan; see
[credits and pricing](https://docs.ortex.com/reference/credits-and-pricing).

## Try it

- "Use ORTEX — is GME a short-squeeze setup right now?"
- "Rank NVDA, AMD, PLTR by ORTEX short score."
- "Show the cost-to-borrow trend for AMC over 3 months."

## What's in here

```
.claude-plugin/marketplace.json     # marketplace listing
plugins/ortex/
  .claude-plugin/plugin.json        # plugin manifest
  .mcp.json                         # the ORTEX connector (points at mcp.ortex.com)
  skills/ortex-short-analysis/      # the analyst skill
  skills/get-started/               # what you can ask
```

No secrets, no API keys, no server code live here — just the public connector URL and
the skills. You sign in to ORTEX at connect time; nothing about your account is stored in this repo.

## Also available

- **Claude Desktop / claude.ai:** Settings → Connectors → Add custom connector → `https://mcp.ortex.com`.
- **ChatGPT:** on chatgpt.com in a browser (web only), Plugins → + → Add custom MCP server →
  `https://mcp.ortex.com/mcp` → Create as a plugin. No developer mode needed; available on ChatGPT Pro,
  Business, Enterprise and Edu.

© ORTEX. See LICENSE.
