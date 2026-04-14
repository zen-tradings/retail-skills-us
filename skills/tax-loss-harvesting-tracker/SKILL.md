---
name: tax-loss-harvesting-tracker
description: Identifies and plans tax loss harvesting opportunities across a portfolio. Use when the user asks about tax loss harvesting, wants to find losses to offset gains, asks "how can I reduce my capital gains tax", "which positions should I sell for losses", "wash sale rules", "tax-efficient selling", or mentions offsetting gains with losses. Also triggers when users share portfolio positions with unrealized losses, ask about year-end tax planning for investments, or want to understand how harvesting losses works. Handles wash-sale compliance, replacement security suggestions, and cross-account tracking.
---

# Tax Loss Harvesting Tracker

## Purpose

Systematically identify positions with unrealized losses that can be sold to offset realized gains (or up to $3,000 of ordinary income), while maintaining desired market exposure through replacement securities and staying compliant with wash sale rules.

Tax loss harvesting is the single most reliable source of "alpha" for individual investors — it doesn't require predicting the market, just disciplined tax management. Studies show it can add 1-2% annually in after-tax returns.

---

## Information Gathering

### Required
1. **Current portfolio positions** (ticker, shares, cost basis, purchase date)
   - Accept in any format: screenshot, CSV, typed list, brokerage statement
   - If user uploads a file, parse it
2. **Realized gains/losses this year** (to know how much to harvest)
3. **Filing status and approximate income** (to determine tax benefit of harvesting)

### Helpful
4. **Capital loss carryforward** from prior years
5. **All accounts** (taxable, IRA, 401k, spouse's accounts) — wash sales apply across ALL accounts
6. **State of residence** (state tax benefit adds to savings)

### If User Just Wants to Learn
If the user doesn't have positions to share, explain the concept with examples and walk through a hypothetical scenario.

---

## Analysis Workflow

Copy this checklist into your working response and tick items off as you go:

```
TLH Analysis Progress:
- [ ] Step 1: Identify harvesting candidates (positions at a loss)
- [ ] Step 2: Match losses to gains (apply ordering rules)
- [ ] Step 3: Wash-sale compliance check across ALL accounts (incl. spouse, IRA, DRIP)
- [ ] Step 4: Suggest replacement securities
- [ ] Step 5: Generate action plan with calendar reminders
- [ ] Disclaimers included
```

### Step 1: Identify Harvesting Candidates

Scan all positions in taxable accounts for unrealized losses:

```
For each position:
  Unrealized Gain/Loss = (Current Price - Cost Basis) × Shares
  If Unrealized Loss < 0 → harvesting candidate
  
Sort candidates by:
  1. Largest absolute loss (biggest tax benefit)
  2. Short-term losses first (worth more — offset short-term gains taxed at ordinary rates)
  3. Days until long-term threshold (prioritize harvesting before loss becomes long-term if you have short-term gains to offset)
```

### Step 2: Match Losses to Gains

Apply the tax loss offset ordering rules:
```
1. Short-term losses first offset short-term gains
2. Remaining ST losses offset long-term gains  
3. Long-term losses first offset long-term gains
4. Remaining LT losses offset short-term gains
5. Net losses up to $3,000 offset ordinary income
6. Excess carries forward to future years
```

Calculate the tax savings:
```
Tax Saved = ST Loss Used × (Federal Marginal Rate + State Rate)
          + LT Loss Used × (Federal LTCG Rate + State Rate)  
          + Ordinary Offset × (Federal Marginal Rate + State Rate)
```

### Step 3: Wash Sale Compliance Check

**This is critical — getting this wrong negates the entire benefit.**

For each candidate loss sale, verify:
```
WASH SALE TRIGGERED IF:
  Within 30 days BEFORE or AFTER the sale, you buy:
  - The same security (exact ticker) in ANY account
  - An option on the same security
  - A "substantially identical" security
  
CHECK ALL ACCOUNTS:
  - All taxable brokerage accounts
  - IRAs (Traditional and Roth) — wash sale in IRA is PERMANENT loss
  - Spouse's accounts
  - Automatic dividend reinvestment (DRIP) — turn off DRIP 31 days before sale
  
NOT SUBSTANTIALLY IDENTICAL (safe replacements):
  - Different index funds tracking different indices (e.g., VTI → ITOT)
  - Same sector but different fund family/index
  - Individual stocks are never "substantially identical" to each other
```

### Step 4: Suggest Replacement Securities

For each loss harvest candidate, suggest a replacement that maintains similar exposure without triggering wash sales:

#### Common Swap Pairs

| Sell (Harvest Loss) | Buy (Replacement) | Category |
|---|---|---|
| VOO (Vanguard S&P 500) | IVV or SPLG (iShares/SPDR S&P 500) | S&P 500 |
| VTI (Vanguard Total Market) | ITOT or SCHB (iShares/Schwab Total Market) | US Total Market |
| VXUS (Vanguard Intl) | IXUS or SCHF (iShares/Schwab Intl) | International |
| QQQ (Nasdaq 100) | QQQM (Invesco Nasdaq 100) | Nasdaq 100 |
| VWO (Vanguard EM) | IEMG or SCHE (iShares/Schwab EM) | Emerging Markets |
| BND (Vanguard Total Bond) | AGG or SCHZ (iShares/Schwab Bond) | US Bonds |
| VNQ (Vanguard REIT) | IYR or SCHH (iShares/Schwab REIT) | REITs |
| VUG (Vanguard Growth) | IWF or SCHG (iShares/Schwab Growth) | US Growth |
| VTV (Vanguard Value) | IWD or SCHV (iShares/Schwab Value) | US Value |
| Individual Stock | Different stock in same sector | Sector exposure |

**Important**: After 31 days, the user can swap back to their original fund if preferred.

### Step 5: Generate Action Plan

---

## Output Format

### Harvesting Opportunities Summary

```
CURRENT YEAR STATUS
Realized Short-Term Gains:     $X,XXX
Realized Long-Term Gains:      $X,XXX
Realized Losses:               ($X,XXX)
Net Position:                  $X,XXX gain / ($X,XXX) loss

HARVESTING CANDIDATES (sorted by tax savings)

#1: [TICKER] — [Company/Fund Name]
    Shares: XXX | Basis: $XX.XX | Current: $XX.XX
    Unrealized Loss: ($X,XXX) [Short-Term / Long-Term]
    Est. Tax Savings: $X,XXX
    Replacement: [TICKER] ([Name]) — [brief reason it maintains exposure]
    Wash Sale Risk: [None / Check DRIP / Check IRA holdings]

#2: [TICKER] — ...
    ...

TOTAL POTENTIAL TAX SAVINGS: $X,XXX

ACTION STEPS:
1. Turn off DRIP for [tickers] if enabled
2. Sell [list] in taxable account on [date]
3. Immediately buy [replacements]  
4. Set calendar reminder: [date + 31 days] — safe to swap back
5. Do NOT buy [original tickers] in any account until [date + 31 days]
```

### Year-End Planning View (when asked in Oct-Dec)

```
YEAR-END TAX POSITION
                          Realized    Unrealized    After Harvest
Short-Term Gains:         $X,XXX      $X,XXX        $X,XXX
Short-Term Losses:        ($X,XXX)    ($X,XXX)      ($X,XXX)
Long-Term Gains:          $X,XXX      $X,XXX        $X,XXX
Long-Term Losses:         ($X,XXX)    ($X,XXX)      ($X,XXX)
─────────────────────────────────────────────────────────────
Net Capital Gain/Loss:    $X,XXX                    $X,XXX
Ordinary Income Offset:                             ($3,000)
Loss Carryforward:                                  ($X,XXX)

ESTIMATED TAX SAVINGS FROM HARVESTING: $X,XXX
```

---

## Strategic Considerations

### When to Harvest
- **Year-end** (Nov-Dec): Most common, final chance before tax year closes
- **Market downturns**: Best opportunities arise during broad selloffs
- **Throughout the year**: More sophisticated; capture losses as they appear
- **Before a big gain**: If you're planning to sell a winner, harvest losses first

### When NOT to Harvest
- **Loss is too small**: Transaction costs and complexity may not be worth it for <$100 savings
- **Position you want to hold forever**: Harvesting resets your holding period and basis; if you intend to hold until death (step-up basis), harvesting is counterproductive
- **Wash sale trap**: If you can't avoid repurchasing within 30 days (e.g., 401k auto-contributions buying same fund)
- **In a 0% LTCG bracket**: If your income is low enough for 0% LTCG rate, the loss has less value

### Advanced: Direct Indexing
For portfolios > $100,000, mention direct indexing as the ultimate tax loss harvesting approach:
- Own individual stocks instead of an index fund
- Harvest losses on individual stocks while maintaining index-like exposure
- Services like Wealthfront, Betterment, Fidelity offer this
- Can generate significantly more harvesting opportunities than ETF swaps

---

## Cross-Account Wash Sale Scenarios

These are the tricky situations to flag:

1. **401(k) auto-buy**: User sells VTI in taxable but 401(k) buys a total market fund every paycheck → potential wash sale
2. **Spouse's account**: Spouse has same stocks → wash sale applies
3. **DRIP reinvestment**: Automatic reinvestment buys shares within 30-day window
4. **IRA wash sale**: If wash sale triggered via IRA purchase, the loss is PERMANENTLY disallowed (not added to IRA basis) — this is the worst outcome

Always ask: "Do you have automatic purchases in a 401(k) or IRA that might buy similar funds?"

---

## Important Disclaimers

- Tax loss harvesting reduces taxes now but may increase taxes later (lower basis on replacement)
- The benefit is primarily tax deferral, not elimination (unless assets are held until death for step-up)
- Wash sale rules are complex; consult a tax professional for your specific situation
- "Substantially identical" has no precise IRS definition for funds — the swap pairs above are widely accepted but not guaranteed

---

## Reference Data

Read `references/tax-rates-2025.md` for current tax rates to calculate savings accurately.
