---
name: portfolio-rebalance-tax-calc
description: Calculates the tax cost of rebalancing a portfolio and finds the most tax-efficient path from the current allocation to a target allocation. Use when the user asks about rebalancing, adjusting asset allocation, "how to rebalance without paying too much tax", "tax-efficient rebalancing", "change my allocation from X to Y", "reduce my stock exposure", "move money from stocks to bonds", or any question about changing portfolio weights while minimizing taxes. Also triggers when users mention being overweight or underweight in something, want to de-risk, or are considering a major portfolio restructuring. Covers multi-account rebalancing, tax-lot optimization, and phased transition plans.
---

# Portfolio Rebalance Tax Calculator

## Purpose

Rebalancing is necessary to maintain your target allocation, but selling winners in a taxable account triggers capital gains taxes. This skill finds the path from current allocation to target allocation that minimizes the tax bill — often saving thousands of dollars through smart sequencing, account selection, and lot optimization.

The naive approach (sell everything overweight, buy everything underweight) can be extremely costly. A tax-aware approach might achieve the same result at a fraction of the tax cost.

---

## Information Gathering

### Required
1. **Current portfolio**: All positions across all accounts with:
   - Ticker, shares, current value
   - Cost basis and purchase date (for taxable accounts)
   - Account type (Taxable, Traditional IRA, Roth IRA, 401k)
2. **Target allocation**: What they want to move to (e.g., 60/40 stocks/bonds, specific fund targets)

### Needed for Tax Calculation
3. **Filing status** and **estimated taxable income**
4. **State of residence**
5. **Realized gains/losses this year** already

### Helpful
6. **Expected new contributions** (401k, IRA) — can use these to rebalance without selling
7. **Timeline**: Urgent (do it now) vs. gradual (over months/year)
8. **Cash available to deploy**
9. **Capital loss carryforward**

---

## Rebalancing Strategies (Ranked by Tax Efficiency)

### Strategy 1: Contribution-Based Rebalancing (Zero Tax Cost)
```
Direct new money to underweight asset classes:
- 401(k) contributions → buy underweight funds
- IRA contributions → buy underweight funds
- New cash savings → buy underweight funds in taxable

Tax Cost: $0
Timeline: Slow (depends on contribution amounts)
Best For: Small imbalances, patient investors
```

### Strategy 2: Tax-Advantaged Account Rebalancing (Zero Tax Cost)
```
Sell/buy within IRA or 401(k) only — no tax consequences:
- Sell overweight positions in IRA/401(k)
- Buy underweight positions in IRA/401(k)

Tax Cost: $0
Timeline: Immediate
Limitation: Only rebalances the tax-advantaged portion; taxable account unchanged
```

### Strategy 3: Dividend/Distribution Redirect (Zero Tax Cost)
```
Redirect dividends and capital gains distributions:
- Turn off reinvestment (DRIP) on overweight positions
- Use the cash to buy underweight positions

Tax Cost: $0 (dividends are taxed regardless)
Timeline: Gradual
Best For: High-yield portfolios
```

### Strategy 4: Tax Loss Harvesting Rebalance (Negative Tax Cost!)
```
Sell positions that have losses AND are overweight:
- Realize the loss (tax benefit)
- Buy target allocation with proceeds
- Net result: rebalanced AND reduced taxes

Tax Cost: Negative (you save money)
Best For: After market downturns
```

### Strategy 5: Selective Lot Selling (Minimized Tax Cost)
```
When you must sell in taxable:
- Sell highest-cost-basis lots first (smallest gain)
- Sell long-term lots before short-term lots
- Sell loss lots first (tax benefit)
- Avoid lots approaching long-term status (wait if possible)

Tax Cost: Minimized through lot selection
```

### Strategy 6: Asset Location Shift (Gradual, Tax-Efficient)
```
Over time, restructure which assets are in which accounts:
- Taxable: Hold tax-efficient assets (US index ETFs, munis)
- Tax-Advantaged: Hold tax-inefficient assets (bonds, REITs, intl)
- Gradually make swaps when opportunities arise

Tax Cost: Depends on execution
Timeline: 1-3 years
```

---

## Calculation Workflow

Copy this checklist into your working response and tick items off as you go:

```
Rebalance Tax Plan Progress:
- [ ] Step 1: Map current vs target allocation
- [ ] Step 2: Identify zero-tax rebalancing moves (IRA / 401k / contributions / DRIP)
- [ ] Step 3: Optimize taxable-account sales (lot selection)
- [ ] Step 4: Calculate total rebalancing tax cost (compare options A / B / C)
- [ ] Step 5: Generate phased action plan
- [ ] Disclaimers included
```

### Step 1: Map Current vs. Target

```
                    Current     Target      Difference
US Stocks:          $XXX (XX%)  $XXX (XX%)  +/-$X,XXX (over/underweight)
Intl Stocks:        $XXX (XX%)  $XXX (XX%)  +/-$X,XXX
US Bonds:           $XXX (XX%)  $XXX (XX%)  +/-$X,XXX
Intl Bonds:         $XXX (XX%)  $XXX (XX%)  +/-$X,XXX
REITs:              $XXX (XX%)  $XXX (XX%)  +/-$X,XXX
Cash:               $XXX (XX%)  $XXX (XX%)  +/-$X,XXX
```

### Step 2: Identify Zero-Tax Rebalancing Opportunities

Before selling anything in taxable, exhaust these options:
```
Available Zero-Tax Moves:
1. Rebalance within IRA:           Can shift $X,XXX
2. Rebalance within 401(k):        Can shift $X,XXX
3. Redirect next contributions:    $X,XXX/month available
4. Redirect dividends:             $X,XXX/quarter available
5. Deploy available cash:          $X,XXX available

After zero-tax moves:
  Remaining imbalance: $X,XXX to rebalance in taxable account
```

### Step 3: Optimize Taxable Account Sales

For the remaining imbalance that requires selling in taxable:

```
For each overweight position in taxable:
  List all tax lots sorted by tax efficiency:
  
  Lot   Shares  Basis    Current  Gain/Loss  Type    Tax Cost
  1     100     $45.00   $80.00   $3,500     LT      $525
  2     50      $72.00   $80.00   $400       LT      $60
  3     75      $85.00   $80.00   ($375)     ST      -$131 (savings!)
  
  SELL ORDER: Lot 3 first (loss), Lot 2 next (small LT gain), Lot 1 last
```

### Step 4: Calculate Total Rebalancing Tax Cost

```
REBALANCING TAX ANALYSIS

Option A: Naive Rebalance (sell proportionally)
  Sales Required:            $XX,XXX
  Realized Gains:            $XX,XXX
  Federal Tax:               $X,XXX
  State Tax:                 $X,XXX
  Total Tax Cost:            $X,XXX

Option B: Tax-Optimized Rebalance
  Zero-tax moves:            $XX,XXX rebalanced (no tax)
  Taxable sales (lot-optimized): $XX,XXX
  Realized Gains:            $XX,XXX
  Realized Losses:           ($X,XXX)
  Net Taxable:               $XX,XXX
  Federal Tax:               $X,XXX
  State Tax:                 $X,XXX
  Total Tax Cost:            $X,XXX

Option C: Phased Rebalance (over X months)
  Phase 1 (now):             Zero-tax moves + loss harvesting
  Phase 2 (contributions):   Direct $X,XXX/month to underweight
  Phase 3 (after lots go LT): Sell $XX,XXX in LT lots
  Total Tax Cost:            $X,XXX
  Timeline:                  X months to target

TAX SAVINGS: Option B saves $X,XXX vs Option A
             Option C saves $X,XXX vs Option A
```

### Step 5: Generate Action Plan

```
RECOMMENDED REBALANCING PLAN

IMMEDIATE (this week):
□ Rebalance within 401(k): Sell $X of [Fund], Buy $X of [Fund]
□ Rebalance within IRA: Sell $X of [Fund], Buy $X of [Fund]
□ Sell [TICKER] Lot #3 (loss harvest): $X,XXX
□ Buy $X,XXX of [underweight fund] with proceeds

THIS MONTH:
□ Turn off DRIP on [overweight tickers]
□ Change 401(k) contributions to 100% [underweight fund]
□ Deploy $X,XXX cash to [underweight fund]

WITHIN 3 MONTHS:
□ Wait for [TICKER] lots to reach long-term status on [DATE]
□ Then sell $X,XXX of long-term lots
□ Buy $X,XXX of [target fund]

ONGOING:
□ Direct all new savings to [underweight asset class]
□ Review allocation quarterly
□ Target completion date: [DATE]
```

---

## Rebalancing Bands (When to Rebalance)

Help users set up rebalancing triggers:

```
Common Approach: Rebalance when any asset class drifts >5% from target

Target   Band         Rebalance Trigger
60%      55-65%       If stocks drop below 55% or exceed 65%
30%      25-35%       If bonds drop below 25% or exceed 35%
10%      5-15%        If intl drops below 5% or exceeds 15%

Tax-Aware Modification:
- Only rebalance using tax-free methods unless drift exceeds 10%
- Harvest losses opportunistically when they appear
- Use calendar-year boundaries strategically
```

---

## Special Scenarios

### Major Allocation Change (e.g., 90/10 → 60/40)
When someone wants a large shift, a phased approach is almost always better:
- Phase over 6-12 months
- Prioritize selling losses and highest-basis lots
- Use new contributions aggressively
- Consider if the urgency justifies the tax cost

### Concentrated Stock Position
When someone has too much in a single stock (e.g., employer stock):
- Sell in annual tranches to manage bracket impact
- Pair with loss harvesting in other positions
- Consider charitable giving of appreciated shares
- Look into exchange funds or protective puts (advanced)

### Post-Retirement Rebalancing
Different considerations when in retirement:
- May be in lower tax bracket (more room for gains)
- Required Minimum Distributions (RMDs) force traditional IRA sales
- Use RMDs to rebalance (direct to underweight assets)
- Roth conversions can be combined with rebalancing strategy

### Tax-Gain Harvesting
In low-income years (job loss, sabbatical, early retirement):
- Intentionally realize long-term gains while in 0% LTCG bracket
- Reset cost basis to higher level for free
- Opposite of tax-loss harvesting — equally valuable

---

## Important Disclaimers

- This analysis is for planning purposes; actual taxes depend on complete tax situation
- Tax lot information should be verified against brokerage statements
- Rebalancing involves investment risk — selling one asset to buy another exposes you to timing risk
- Wash sale rules apply when selling at a loss and buying similar securities within 30 days
- Consult a tax professional before making major portfolio changes

---

## Reference Data

Read `references/tax-rates-2025.md` for current tax rates. The capital-gains-estimator skill can be used for detailed gain/loss calculations on individual positions. The tax-loss-harvesting-tracker skill can identify loss harvesting opportunities as part of the rebalancing process.
