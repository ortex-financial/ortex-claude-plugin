---
name: get-started
description: Introduce the ORTEX plugin. Use when the user has just added ORTEX, asks what ORTEX can do here, what data is available, or how to start using it.
---

# Get started with ORTEX

ORTEX is connected through its tools (names start with `get_`, plus
`ortex_getting_started` and `ortex_data_catalog`). All of them only read data.

## What to do

1. Call `ortex_getting_started` once. It returns what ORTEX covers and which
   datasets each plan level includes.
2. Tell the user, in three or four lines, what they can ask about:
   - short selling: short interest, cost to borrow, days to cover, availability, short score;
   - options: chains, Greeks, put/call ratios;
   - scores, peers and US government (Congress) trades;
   - fundamentals, prices, free float, splits, earnings and macro calendars;
   - ETFs: holdings, and which ETFs hold a stock.
3. Offer two or three example questions, for example:
   - "How heavily shorted is GME right now, and what does it cost to borrow?"
   - "Compare short interest and days to cover for TSLA, NVDA and AMD."
   - "Which ETFs hold the most NVDA?"

## Ground rules

- ORTEX is read-only. It cannot place trades, move money or change the user's account.
- It is data and analysis, not personal investment advice.
- The data returned is what the user's ORTEX plan includes. If a tool says a
  dataset is not included, say so plainly and relay its explanation. Do not
  suggest buying or changing a plan.
- Use `get_exchanges` when the exchange for a ticker is unclear.
