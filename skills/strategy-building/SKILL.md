---
name: strategy-building
description: Turn a vague investment goal OR a set of specific stock picks into a concrete, executable retail investment strategy. Use this skill in two scenarios. (A) Fuzzy-goal entry — user describes a need like "I want passive income", "I'm scared of losing money", "I have $50k and don't know what to do", "help me build a portfolio", "I want a strategy for my Roth IRA". (B) Thesis-basket entry — user already has specific tickers and wants rules around them, e.g. "I think AXTI, COHR, LITE are promising, how to form a strategy?", "I like these 3 names, how should I play them?", "how do I turn this watchlist into a plan?", "I want to build a thematic basket around AI/energy/biotech". Also trigger on "design", "build", "create", or "pick" a strategy, ETF mix, basket, or allocation, and on "what should I invest in". The skill interviews the user, picks the appropriate branch, and produces a written spec with explicit rules (universe, entry, sizing, rebalance cadence, exit, guardrails) that the user — or another skill — can execute.
---

# Strategy Building

## Purpose

Convert a blurry investment need into a written strategy spec that is concrete enough to follow mechanically. Retail investors often know *what they want* (income, growth, safety) but not *what to actually do on Monday morning*. This skill bridges that gap by forcing every strategy through the same structured interview and producing a consistent, reviewable artifact.

The output is a **spec, not code** — a document the user can execute manually, hand to an advisor, or pass to another skill (e.g., `portfolio-rebalance-tax-calc`) for tax-aware execution.

---

## Information Gathering

Do not skip the interview. A strategy built on assumed inputs is worse than no strategy.

### Required
1. **Goal** — what is the money *for*? (retirement in 25 years, house down payment in 3 years, passive income now, generic growth)
2. **Horizon** — when will the user need to spend it? Convert vague answers ("eventually") into a range.
3. **Capital** — amount to invest now, plus any recurring contributions
4. **Account type** — taxable brokerage, Roth IRA, Traditional IRA, 401(k), HSA (affects tax treatment and available instruments)
5. **Risk tolerance** — not just "low/medium/high". Ask: "If this dropped 30% next year, would you sell, hold, or buy more?"

### Helpful
6. **Existing holdings** — to avoid concentration or duplication
7. **Income & filing status** — affects after-tax math and contribution limits
8. **Hard constraints** — ESG exclusions, no-single-stocks rule, employer stock restrictions, liquidity needs
9. **Experience level** — determines how much explanation to include and whether to warn against complex instruments

### If the user is fuzzy
Offer **concrete choices** instead of open questions. E.g., instead of "what's your risk tolerance?", ask: "Pick one — (A) I'd panic-sell in a 30% drawdown, (B) I'd hold but lose sleep, (C) I'd buy more." Fuzzy users answer multiple-choice better than essays.

---

## Strategy Design Workflow

### Step 0: Pick the entry branch

Before anything else, determine which starting point the user is at:

- **Branch A — Fuzzy goal, no picks.** User has a need but no specific instruments in mind. ("I want passive income", "help me build a portfolio.") → go to Step 1A.
- **Branch B — Thesis basket, specific picks.** User already has named tickers or a thematic idea and wants rules around them. ("I think AXTI, COHR, LITE are promising, how should I play them?") → go to Step 1B.

If the user lands somewhere in between — e.g., "I want growth and I already own some NVDA" — run **Branch A for the core allocation**, then treat the existing picks as a **Branch B satellite** sub-strategy, sized and capped separately. Do not mix a thesis basket into a core allocation silently.

---

### Step 1A: Classify the goal (Branch A)
Map the stated goal to one of these archetypes. If it doesn't fit cleanly, ask clarifying questions until it does.

| Archetype | Typical horizon | Core vehicle |
|---|---|---|
| **Long-term growth** | 10+ years | Diversified equity index funds |
| **Income generation** | Any | Dividend/bond/REIT mix, covered calls |
| **Capital preservation** | <3 years | Treasuries, HYSA, short-term bonds |
| **Balanced** | 5–15 years | Target-date or stock/bond split |
| **Speculative / thematic** | Any | Satellite allocation only, capped |

Then continue to Step 2.

---

### Step 1B: Thesis basket workflow (Branch B)

When the user arrives with specific picks, do not skip straight to sizing rules. Work through these sub-steps in order — each one is a question the user must answer on the record before the spec is written.

#### 1B.1 — Articulate the thesis
Force the user to state, in one sentence, **why** each ticker is in the basket. Vague answers ("it's hot", "my friend said") are a red flag — push back until the thesis is concrete enough to be disproven. Good thesis statements sound like:
- "COHR and LITE benefit from AI-driven optical interconnect demand in hyperscaler datacenters."
- "AXTI is leveraged to compound semiconductor growth via InP and GaAs wafer supply."

If the user cannot articulate a thesis, **stop and say so** — tell them a basket without a thesis is a gamble, not a strategy, and offer to re-enter via Branch A instead.

#### 1B.2 — Check concentration and correlation
Look at the tickers together and assess whether the "basket" is actually diversified or is a single-factor bet in disguise.

- **Sector/sub-industry overlap** — are they all in the same GICS sub-industry? (Example: AXTI, COHR, LITE are all **photonics / optical components**; a 3-stock basket here is ~1 concentrated bet, not 3 independent bets.)
- **Shared demand driver** — do they all depend on the same macro story (AI capex, oil prices, interest rates, a single customer)? If yes, the basket's effective diversification is close to 1 name.
- **Size / liquidity skew** — is one name a small-cap that will dominate volatility? Mixing a $300M-cap and a $30B-cap in an equal-weight basket means the small name drives most of the risk.

**State these findings to the user explicitly.** Do not silently proceed. The user needs to either (a) accept the concentration consciously, (b) add names to broaden the thesis, or (c) cap the basket size to reflect the true risk.

#### 1B.3 — Decide the portfolio role
A thesis basket can occupy wildly different roles, with wildly different rules:

| Role | % of total portfolio | Rules look like |
|---|---|---|
| **Core conviction** | 20–60% | Long holding period, thesis-driven exits, rebalance rare |
| **Satellite / tactical** | 5–20% | Capped, explicit stop rules, rebalance on schedule |
| **Lottery ticket** | <5% | Accept 100% loss, no averaging down, predefined exit |

The user must **pick one before continuing**. The same 3 tickers produce a completely different spec depending on which role they fill. Default to **Satellite / tactical** if the user is unsure — it is the safest starting point for a retail investor with a thematic bet.

#### 1B.4 — Size the basket and the positions within it
Two levels of sizing:

1. **Total basket size** — the % of total portfolio capital the whole basket gets, bounded by the role cap from 1B.3.
2. **Within-basket weights** — how much each ticker gets of the basket. Offer the user four options and let them pick:
   - **Equal weight** (1/N) — simplest, no implicit conviction ranking, rebalances against winners
   - **Conviction weight** — user ranks 1–5; weights proportional to rank. Requires honest self-assessment.
   - **Market-cap weight** — closest to "buying the sub-sector"; larger names dominate
   - **Risk-parity (volatility-inverse)** — requires recent volatility data; advanced, usually unnecessary at 3 names

Also set a **max single-name cap** (e.g., no one ticker > 50% of the basket) so a runaway winner doesn't quietly turn the basket into a single-stock bet.

#### 1B.5 — Define entry path
- **Lump sum** — defensible only when the thesis is time-sensitive (a specific catalyst) and the user accepts timing risk
- **Scale in over N tranches** — default for retail; reduces regret if the first entry is poorly timed
- **Trigger-based entry** — only buy on a defined pullback or technical level; requires the user to commit to actually executing, not waiting forever

#### 1B.6 — Define thesis-invalidation exits
This is the most important step and the one retail investors skip most. For **each** ticker, the user must name at least one concrete invalidation trigger. Examples:
- "Sell if the next earnings report shows datacenter optical revenue declining YoY."
- "Sell if management guides down gross margin below 35% for two consecutive quarters."
- "Sell if the stock breaks below the 200-day moving average and stays there for 30 days."
- "Reassess if the core thesis (AI optical interconnect demand) is publicly refuted by a major hyperscaler capex cut."

Then add a **portfolio-level stop**: a total drawdown on the basket (e.g., -25%) at which the entire basket is re-reviewed — not auto-sold, but re-reviewed with fresh eyes.

A ticker **without** a written invalidation trigger does not go into the spec. Send the user back to 1B.1 until they produce one.

#### 1B.7 — Consider hedging (optional)
For baskets in the 20%+ role-size range, raise hedging as an option, not a requirement:
- **Sector-ETF short or put** against the closest matching ETF (e.g., an optical/semi sub-sector ETF) to isolate idiosyncratic exposure
- **Portfolio-level protective puts** on SPY/QQQ during high-VIX periods
- **Position trimming** as a cheap alternative to derivatives

Most retail investors should skip this and just size the basket smaller. Mention it, don't push it.

Then continue to Step 2.

### Step 2: Set the allocation

**Branch A** — translate archetype + risk tolerance + horizon into a top-level asset mix. Use simple anchors:
- **Aggressive** (long horizon, high tolerance): 90/10 or 100/0 stocks/bonds
- **Moderate**: 60/40 or 70/30
- **Conservative**: 40/60 or 30/70
- **Preservation**: 20/80 or all short-duration fixed income

Adjust for account type — tax-inefficient assets (bonds, REITs) belong in tax-advantaged accounts when possible.

**Branch B** — the allocation question becomes: "what does the rest of the portfolio look like, and does this basket fit inside it?" Ask the user what they already hold. If they have no core portfolio, **stop and run Branch A first** to build one, then slot the basket into it. A thesis basket with no surrounding portfolio is not a strategy, it's the entire portfolio — flag this explicitly.

### Step 3: Pick the universe
Concrete instruments, not asset-class labels. Prefer:
- **Broad-market, low-cost ETFs** as defaults (e.g., total-market, total-international, aggregate bond)
- **Single stocks** only if the user has an informed view and accepts concentration risk
- **Complex products** (leveraged ETFs, options, crypto) only if explicitly requested, capped, and with written risk warnings

Note tickers but flag that final selection depends on what's available in the user's account.

### Step 4: Define execution rules
The strategy must answer all of these explicitly:
- **Entry** — lump sum now, or dollar-cost average over N months?
- **Position sizing** — what % of total capital per holding? Max single-position cap?
- **Rebalance cadence** — time-based (quarterly, annually) or threshold-based (when drift > 5%)?
- **Contribution rule** — where do new deposits go? (Usually: to the most under-weight bucket)
- **Exit / review triggers** — life event, goal reached, thesis broken, or scheduled annual review?

### Step 5: Add guardrails
Every strategy needs failure modes named up front:
- **Max drawdown the user will tolerate before re-evaluating** (not selling — re-evaluating)
- **Behavioral rules** — e.g., "no trades in the first 48 hours after reading financial news"
- **Tax guardrails** — holding period awareness, wash-sale awareness if harvesting
- **What would make you abandon this strategy?** — the user must name it before starting, not after losing money

### Step 6: Write the spec
Output a single document. Use the section set that matches the branch.

**Branch A (fuzzy-goal) spec:**
```
# Strategy: <name>
## Goal
## Horizon & Capital
## Account(s)
## Asset Allocation
## Universe (specific instruments)
## Execution Rules
  - Entry
  - Sizing
  - Rebalance
  - Contributions
  - Exit / Review
## Guardrails
## Open Questions
```

**Branch B (thesis-basket) spec:**
```
# Strategy: <basket name>
## Thesis (one sentence, plus per-ticker rationale)
## Portfolio Role (core / satellite / lottery, with % cap)
## Concentration Findings (sector overlap, shared drivers, size skew)
## Basket Composition (tickers + within-basket weights + max single-name cap)
## Execution Rules
  - Entry path (lump sum / scale-in / trigger-based)
  - Rebalance cadence or drift rule
  - Add / trim rules
## Invalidation Triggers (per ticker + basket-level drawdown stop)
## Hedging (if any)
## Guardrails
## Open Questions
```

**Open Questions** is mandatory in both branches — list anything the user was vague about so they know what's still assumed.

---

## Quality Checks

Before presenting the spec, verify:
- [ ] Every rule is mechanical — a stranger could execute it without asking the user questions
- [ ] Risk level matches the user's stated tolerance, not what *you* think is prudent
- [ ] No instruments the user doesn't understand are included without a warning
- [ ] Tax treatment is consistent with the account type
- [ ] The strategy is boring — if it sounds exciting, you probably over-designed it

**Branch B extra checks:**
- [ ] Every ticker has a written thesis and a written invalidation trigger
- [ ] Sector/driver overlap has been named out loud, even if the user chose to accept it
- [ ] The basket has a portfolio role (core / satellite / lottery) and respects that role's cap
- [ ] A max single-name cap is set so a winner can't silently eat the basket
- [ ] The basket size is honest about effective concentration — 3 names in one sub-industry is not 3 bets

---

## Handoff to Other Skills

After producing the spec, suggest relevant follow-ups:
- `portfolio-rebalance-tax-calc` — when it's time to rebalance a taxable account
- `capital-gains-estimator` — to estimate tax cost of any initial repositioning
- `tax-loss-harvesting-tracker` — for ongoing tax management
- `etf-tax-efficiency-scorer` — to compare candidate ETFs before finalizing the universe

---

## Reference Data

Read `references/tax-rates-2025.md` when tax treatment affects asset location decisions (e.g., whether bonds belong in the taxable or tax-advantaged account).

---

## What this skill does NOT do

- **Backtest** strategies — the spec is forward-looking; historical validation is a separate task
- **Generate code** — output is a written spec, not a script or notebook
- **Endorse or validate stock picks** — in Branch B the skill builds rules *around* the user's picks; it does not tell the user whether the picks are good. If asked "is this a good trade?", redirect: "I can help you turn it into a disciplined strategy, but I won't call the trade for you."
- **Give personalized financial advice** — always remind the user this is an educational framework, not a recommendation, and encourage consulting a fiduciary for large decisions
