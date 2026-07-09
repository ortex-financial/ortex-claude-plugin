# ORTEX for Claude — plugin

Institutional **short-selling and market-intelligence data** inside Claude — the
short interest, cost-to-borrow and squeeze signals desks pay for — plus an analyst
skill that teaches Claude how to read them.

This repo is a **Claude plugin marketplace**. Installing the plugin gives you:

- **The ORTEX connector** — 27 tools for short interest, cost-to-borrow, days-to-cover,
  options analytics, stock scores, Congressional trades, fundamentals, prices and more,
  via the remote MCP server at `mcp.ortex.com`.
- **The short-analysis skill** — securities-lending methodology so Claude reads the data
  like an analyst (squeeze setups, how to combine CTB + DTC + utilisation, clean output).

## Install (Claude Code)

```
/plugin marketplace add ortex-financial/ortex-claude-plugin
/plugin install ortex
```

Then authorise ORTEX when prompted (log in and click **Authorize**, or paste an API key).
Create a key at [app.ortex.com/apis](https://app.ortex.com/apis); short-selling data needs a Pro plan.

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
```

No secrets, no API keys, no server code live here — just the public connector URL and
the skill. Your ORTEX key is entered at connect time and never stored in this repo.

## Also available

- **Claude Desktop / ChatGPT:** add `https://mcp.ortex.com` as a custom connector.

© ORTEX. See LICENSE.
