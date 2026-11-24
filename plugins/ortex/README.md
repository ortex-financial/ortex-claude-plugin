# ORTEX

ORTEX short-selling and market data in Claude.

The plugin connects Claude to the ORTEX remote MCP server at `https://mcp.ortex.com/mcp`
(34 read-only tools) and adds two skills:

- `ortex-short-analysis`: how to read short interest, cost to borrow, days to cover and
  availability together, and present a short verdict with the evidence and its as-of date.
- `get-started`: what ORTEX covers and example questions.

You sign in with your ORTEX account when Claude first connects. The data you can read is
what your ORTEX plan includes. Everything is read-only: ORTEX never places trades or moves
money, and it does not give personal investment advice.

Try: "How heavily shorted is GME right now, and what does it cost to borrow?"

Documentation: https://docs.ortex.com. Support: https://public.ortex.com/contact
