---
name: ortex-short-analysis
description: Methodology for reading short interest, short-squeeze risk, cost-to-borrow and securities-lending signals using ORTEX data. Use whenever the user asks how heavily a stock is shorted, about short-squeeze risk or setups, borrow costs, days to cover, availability, how crowded the short side is, or wants a short-selling read on a ticker or watchlist.
---

# ORTEX short-selling analysis

You have live ORTEX data through the ORTEX tools (names start with `get_`). This
skill is how to use it like a securities-lending analyst: not just fetch numbers,
but read them together.

## Which tools for which question

| The user asks… | Call |
|---|---|
| How shorted is X / short interest | `get_short_interest` (shares short, % of free float) |
| Squeeze risk / is it a squeeze setup | `get_short_interest` + `get_days_to_cover` + `get_cost_to_borrow` + `get_short_score` (read together) |
| Is it expensive or hard to short | `get_cost_to_borrow` (trend over level) + `get_short_availability` |
| How long to cover / short ratio | `get_days_to_cover` |
| One-number read | `get_short_score` (0–100 composite) |
| Regulatory / official short interest | `get_official_short_interest` (US/CA/AU/HK), `get_european_short_filings` (EU) |
| Screen a watchlist | loop `get_short_score` per ticker |
| Options positioning | `get_options_pcr_sentiment`, `get_options_chain` |

If unsure of the exchange, resolve it with `get_exchanges` or infer it from
context ("US stock TSLA" → a US exchange).

## Reading the signals

- **Short interest % of free float** is the headline. Rough bands: under 5% low,
  5–15% moderate, 15–30% high, over 30% very high. Always relative to the stock's
  own history and float.
- **Days to cover (DTC)** is short shares ÷ average daily volume: how many days of
  normal volume shorts would need to buy back. Above 5 is meaningful, above 10 is a lot.
- **Cost to borrow (CTB)** is the annualized fee to short. **The trend matters more
  than the level.** Rising CTB means supply is tightening or demand to short is rising.
- **Availability** is how many shares are left to borrow. Very little left means new
  shorts cannot get in easily.
- **Short score** is ORTEX's 0–100 composite of the above. Good for ranking; explain
  the drivers, do not just quote it.

## The squeeze-setup checklist

A classic short-squeeze setup lines up several of these at once:

1. High **short interest % of free float**, preferably rising,
2. High **and rising cost to borrow**,
3. **Little availability** left to borrow,
4. **Rising days to cover**,
5. A catalyst (earnings, news, momentum).

No single metric is a squeeze. Call it a *setup*, weigh the evidence, and be
explicit about what is missing.

## How to present it

1. **Lead with a one-line verdict** ("GME shows a tightening short setup: 24% SI,
   DTC 4.1, CTB up from 6% to 31% this month").
2. Then a compact **evidence table** (metric · value · read).
3. Always **cite the as-of date**: this data moves daily.
4. Be measured. This is analysis to support a decision, not investment advice:
   note the uncertainty and what would change the read. Never tell the user to
   buy, sell or short.

## When a tool cannot return data

An ORTEX tool can decline for different reasons that look similar. **Relay the
tool's own message; never substitute your own guess about the cause.**

- **Out of API credits**: the key and plan are fine, the credit balance is used up.
  The same connection works again once credits are available.
- **Dataset not included in the plan**: the message says the plan linked to this
  connection does not include the data. Say so plainly and pass on the
  documentation link the message gives.
- **Missing or invalid key**: the connection is no longer authorized; the user
  reconnects ORTEX in ChatGPT's settings.

In every case: do not pretend to have the number, do not estimate it from memory,
and do not suggest buying or changing a plan. Offer what is still available
(prices, fundamentals and calendars work with every ORTEX key).
