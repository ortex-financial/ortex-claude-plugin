---
name: ortex-short-analysis
description: Expert methodology for reading short interest, short-squeeze risk, cost-to-borrow and securities-lending signals using ORTEX data. Use whenever the user asks how heavily a stock is shorted, about short-squeeze risk or setups, borrow costs/cost-to-borrow, days-to-cover, utilisation, how crowded or trapped the short side is, or wants a short-selling read on a ticker or watchlist.
---

# ORTEX short-selling analysis

You have live ORTEX data through the ORTEX connector (tools prefixed `get_`). This
skill is how to use it like a securities-lending analyst — not just fetch numbers,
but read them. ORTEX's edge is short-selling and securities-lending data; lean into it.

## Which tools for which question

| The user asks… | Call |
|---|---|
| How shorted is X / short interest | `get_short_interest` (shares short, % of free float) |
| Squeeze risk / is it a squeeze setup | `get_short_interest` + `get_days_to_cover` + `get_cost_to_borrow` + `get_short_score` (read together) |
| Is it expensive/hard to short | `get_cost_to_borrow` (trend > level) + `get_short_availability` |
| How long to cover / short ratio | `get_days_to_cover` |
| One-number read | `get_short_score` (0–100 composite) |
| Regulatory/official short interest | `get_official_short_interest` (US/CA/AU/HK), `get_european_short_filings` (EU) |
| Screen a watchlist / index | `get_index_short_data`, or loop `get_short_score` per ticker |
| Options positioning | `get_options_pcr_sentiment`, `get_options_chain` |

If unsure of the exchange, resolve it (`get_exchanges`) or infer from context ("US stock TSLA" → nasdaq/nyse).

## Reading the signals

- **Short interest % of free float** — the headline. Rough bands: <5% low, 5–15% moderate,
  15–30% high, >30% very high. Always relative to the stock's own history and float.
- **Days to cover (DTC)** — short shares ÷ average daily volume: how many days of normal
  volume shorts would need to buy back. Higher = more trapped. >5 is meaningful, >10 is a lot.
- **Cost to borrow (CTB)** — the annualised fee to short. **The trend matters more than the
  level.** Rising CTB = supply tightening or demand to short rising — a leading signal.
- **Utilisation** — % of lendable supply already on loan. Near 100% means there are almost no
  shares left to borrow → new shorts can't get in and existing ones can't be easily added → squeeze fuel.
- **Short score** — ORTEX's 0–100 composite of the above. Good for ranking; explain the drivers, don't just quote it.

## The squeeze-setup checklist

A classic short-squeeze setup lines up several of these at once:
1. High **SI % of free float** (and preferably rising),
2. High **and rising CTB**,
3. **Utilisation near 100%**,
4. **Rising DTC**,
5. A catalyst (earnings, news, momentum).

No single metric is a squeeze. Call it a *setup*, weigh the evidence, and be explicit about what's missing.

## How to present it

1. **Lead with a one-line verdict** ("GME shows a tightening short setup: 24% SI, DTC 4.1, CTB up 6%→31% this month").
2. Then a compact **evidence table** (metric · value · read).
3. Always **cite the as-of date** — this data moves daily.
4. Be measured. This is decision-support, not advice; note uncertainty and what would change the read.

## When a tool can't return data (diagnose precisely — don't guess)

An ORTEX tool can be blocked for three *different* reasons that look similar but need
different fixes. **Relay the tool's actual message; never substitute your own guess**
(e.g. don't say "you need Pro" when the tool said the key is out of credits):

- **Out of API credits** — the key and plan are fine, the credit balance is just empty.
  The message says so. Point the user to **https://app.ortex.com/apis** to add credits;
  the *same connection resumes working immediately* — they do **not** need to upgrade
  their plan or reconnect.
- **Plan doesn't include the dataset** — the message says the key's plan doesn't cover
  this data. Relay it with the link; suggest `ortex_getting_started` if they ask.
- **Missing/invalid key** — the connector isn't authorised; the message says so.

Prices, fundamentals and calendars are broadly available; the proprietary short-selling
data (short interest, CTB, DTC, scores, options analytics, government trades) needs a paid
ORTEX API plan **and** available credits. If a tool returns any of the messages above,
relay it plainly with the link — don't pretend you have the number, and don't diagnose
the cause yourself beyond what the message says.
