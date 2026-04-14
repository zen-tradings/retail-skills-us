# Thesis Basket Workflow (Branch B)

## Contents
- 1B.1 — Articulate the thesis
- 1B.2 — Check concentration and correlation
- 1B.3 — Decide the portfolio role
- 1B.4 — Size the basket and the positions within it
- 1B.5 — Define entry path
- 1B.6 — Define thesis-invalidation exits
- 1B.7 — Consider hedging (optional)

When the user arrives with specific picks, do not skip straight to sizing rules. Work through these sub-steps in order — each one is a question the user must answer on the record before the spec is written.

## 1B.1 — Articulate the thesis

Force the user to state, in one sentence, **why** each ticker is in the basket. Vague answers ("it's hot", "my friend said") are a red flag — push back until the thesis is concrete enough to be disproven. Good thesis statements sound like:
- "COHR and LITE benefit from AI-driven optical interconnect demand in hyperscaler datacenters."
- "AXTI is leveraged to compound semiconductor growth via InP and GaAs wafer supply."

If the user cannot articulate a thesis, **stop and say so** — tell them a basket without a thesis is a gamble, not a strategy, and offer to re-enter via Branch A instead.

## 1B.2 — Check concentration and correlation

Look at the tickers together and assess whether the "basket" is actually diversified or is a single-factor bet in disguise.

- **Sector/sub-industry overlap** — are they all in the same GICS sub-industry? (Example: AXTI, COHR, LITE are all **photonics / optical components**; a 3-stock basket here is ~1 concentrated bet, not 3 independent bets.)
- **Shared demand driver** — do they all depend on the same macro story (AI capex, oil prices, interest rates, a single customer)? If yes, the basket's effective diversification is close to 1 name.
- **Size / liquidity skew** — is one name a small-cap that will dominate volatility? Mixing a $300M-cap and a $30B-cap in an equal-weight basket means the small name drives most of the risk.

**State these findings to the user explicitly.** Do not silently proceed. The user needs to either (a) accept the concentration consciously, (b) add names to broaden the thesis, or (c) cap the basket size to reflect the true risk.

## 1B.3 — Decide the portfolio role

A thesis basket can occupy wildly different roles, with wildly different rules:

| Role | % of total portfolio | Rules look like |
|---|---|---|
| **Core conviction** | 20–60% | Long holding period, thesis-driven exits, rebalance rare |
| **Satellite / tactical** | 5–20% | Capped, explicit stop rules, rebalance on schedule |
| **Lottery ticket** | <5% | Accept 100% loss, no averaging down, predefined exit |

The user must **pick one before continuing**. The same 3 tickers produce a completely different spec depending on which role they fill. Default to **Satellite / tactical** if the user is unsure — it is the safest starting point for a retail investor with a thematic bet.

## 1B.4 — Size the basket and the positions within it

Two levels of sizing:

1. **Total basket size** — the % of total portfolio capital the whole basket gets, bounded by the role cap from 1B.3.
2. **Within-basket weights** — how much each ticker gets of the basket. Offer the user four options and let them pick:
   - **Equal weight** (1/N) — simplest, no implicit conviction ranking, rebalances against winners
   - **Conviction weight** — user ranks 1–5; weights proportional to rank. Requires honest self-assessment.
   - **Market-cap weight** — closest to "buying the sub-sector"; larger names dominate
   - **Risk-parity (volatility-inverse)** — requires recent volatility data; advanced, usually unnecessary at 3 names

Also set a **max single-name cap** (e.g., no one ticker > 50% of the basket) so a runaway winner doesn't quietly turn the basket into a single-stock bet.

## 1B.5 — Define entry path

- **Lump sum** — defensible only when the thesis is time-sensitive (a specific catalyst) and the user accepts timing risk
- **Scale in over N tranches** — default for retail; reduces regret if the first entry is poorly timed
- **Trigger-based entry** — only buy on a defined pullback or technical level; requires the user to commit to actually executing, not waiting forever

## 1B.6 — Define thesis-invalidation exits

This is the most important step and the one retail investors skip most. For **each** ticker, the user must name at least one concrete invalidation trigger. Examples:
- "Sell if the next earnings report shows datacenter optical revenue declining YoY."
- "Sell if management guides down gross margin below 35% for two consecutive quarters."
- "Sell if the stock breaks below the 200-day moving average and stays there for 30 days."
- "Reassess if the core thesis (AI optical interconnect demand) is publicly refuted by a major hyperscaler capex cut."

Then add a **portfolio-level stop**: a total drawdown on the basket (e.g., -25%) at which the entire basket is re-reviewed — not auto-sold, but re-reviewed with fresh eyes.

A ticker **without** a written invalidation trigger does not go into the spec. Send the user back to 1B.1 until they produce one.

## 1B.7 — Consider hedging (optional)

For baskets in the 20%+ role-size range, raise hedging as an option, not a requirement:
- **Sector-ETF short or put** against the closest matching ETF (e.g., an optical/semi sub-sector ETF) to isolate idiosyncratic exposure
- **Portfolio-level protective puts** on SPY/QQQ during high-VIX periods
- **Position trimming** as a cheap alternative to derivatives

Most retail investors should skip this and just size the basket smaller. Mention it, don't push it.
