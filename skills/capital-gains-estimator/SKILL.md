---
name: capital-gains-estimator
description: Estimate the tax impact of selling investments BEFORE you sell. Use this skill whenever someone asks about selling stocks, ETFs, or other investments and wants to know the tax consequences, or asks "how much tax will I owe", "should I sell now or wait", "what's the tax on my gains", "short-term vs long-term tax difference", "tax impact of selling", or any question about capital gains taxes on a potential or completed sale. Also trigger when users mention holding periods, tax brackets for investments, or comparing after-tax returns. This skill covers federal + state taxes, NIIT, and provides actionable sell/hold recommendations.
---

# Capital Gains Tax Estimator

## Purpose

Help investors understand the exact tax cost of selling an investment BEFORE they execute the trade. Most people are shocked by how much taxes eat into their gains — especially short-term gains in high-tax states. This tool turns a vague "I'll owe some tax" into a precise dollar amount that changes behavior.

## Why This Matters

A $10,000 gain taxed as short-term in California could cost $3,500+ in taxes (federal 22-37% + state 9.3-13.3% + possible 3.8% NIIT). The same gain held one more month to qualify as long-term might cost only $1,500. That difference alone can be worth more than months of market returns.

---

## Information Gathering

Collect these inputs from the user (ask for what's missing, offer defaults where sensible):

### Required
1. **Purchase price** (cost basis) per share or total
2. **Current/target sale price** per share or total
3. **Number of shares** (if per-share prices given)
4. **Purchase date** (to determine holding period)
5. **Planned sale date** (default: today)

### Needed for Accurate Tax Calculation
6. **Filing status**: Single, MFJ, MFS, HoH (default: Single)
7. **Estimated total taxable income** for the year (excluding this sale)
8. **State of residence** (default: ask, matters enormously)

### Optional (for precision)
9. **Other capital gains/losses this year** (affects bracket stacking)
10. **Capital loss carryforward** from prior years

If the user doesn't know their taxable income, help them estimate:
- "Roughly what's your annual salary before taxes?"
- Use salary minus standard deduction as a quick estimate

---

## Calculation Workflow

### Step 1: Determine Gain/Loss
```
Gain = (Sale Price - Cost Basis) × Shares
      - Adjust for any wash sale basis additions
      - Subtract commission/fees if provided
```

### Step 2: Classify Holding Period
```
Days Held = Sale Date - Purchase Date
If Days Held > 365: Long-Term
If Days Held <= 365: Short-Term

IMPORTANT: If close to 1 year, calculate the exact long-term qualification date
and tell the user: "If you wait until [date], this becomes long-term and saves you $X"
```

### Step 3: Calculate Federal Tax

**Short-term gains**: Stack on top of ordinary income, taxed at marginal rate.
```
Marginal Rate = bracket that (Taxable Income + Gain) falls into
Federal Tax = Gain × Marginal Rate
Note: gain may span multiple brackets — calculate each tranche
```

**Long-term gains**: Use preferential rates (0% / 15% / 20%).
```
Use taxable income to determine starting LTCG bracket
Stack the gain on top to see if it crosses bracket thresholds
Calculate tax on each tranche at the applicable rate
```

### Step 4: Calculate NIIT (if applicable)
```
If MAGI > threshold ($200K single / $250K MFJ):
  NIIT = min(Net Investment Income, MAGI - threshold) × 3.8%
```

### Step 5: Calculate State Tax
Read the user's state from references/tax-rates-2025.md.
- Most states tax capital gains as ordinary income (including California)
- Some states have no income tax (TX, FL, NV, WA, TN, WY, AK, SD, NH)
- Washington state: 7% tax on LTCG > $270,000

### Step 6: Total Tax & Effective Rate
```
Total Tax = Federal + NIIT + State
Effective Rate = Total Tax / Gain × 100
After-Tax Proceeds = Sale Price × Shares - Total Tax
```

---

## Output Format

Present results clearly with these sections:

### Summary Table
```
Sale Proceeds:          $XX,XXX
Cost Basis:             $XX,XXX
Capital Gain:           $XX,XXX
Holding Period:         X days (Short-Term / Long-Term)

Federal Tax:            $X,XXX  (XX.X%)
NIIT:                   $X,XXX  (3.8% if applicable)
State Tax ([State]):    $X,XXX  (XX.X%)
─────────────────────────────────
Total Tax:              $X,XXX
Effective Tax Rate:     XX.X%
After-Tax Gain:         $X,XXX
```

### Hold vs. Sell Comparison (when near 1-year mark)
If the holding period is between 10-12 months, ALWAYS show:
```
                    Sell Now (Short-Term)    Wait Until [Date] (Long-Term)
Federal Tax:        $X,XXX                  $X,XXX
State Tax:          $X,XXX                  $X,XXX
Total Tax:          $X,XXX                  $X,XXX
Tax Savings:                                $X,XXX
Break-Even:         Stock can drop X.X% and you still come out ahead waiting
```

### Actionable Insight
Always end with one of these:
- **Near 1-year**: "Waiting X more days saves $Y in taxes. The stock would need to drop Z% to make selling now worthwhile."
- **Large short-term gain**: "This gain is taxed at your top marginal rate of X%. Consider whether this position will be held into next year."
- **In 0% LTCG bracket**: "Good news — at your income level, this long-term gain is taxed at 0% federally."
- **Loss scenario**: "This $X loss can offset gains and up to $3,000 of ordinary income, saving you approximately $Y."
- **Multiple lots**: "Consider selling specific lots — selling the highest-cost-basis shares first minimizes your taxable gain."

---

## Multi-Lot Handling

If the user has bought the same stock at different times/prices:

1. Ask which cost basis method they use (FIFO, specific identification, average cost for mutual funds)
2. Show the tax impact of selling different lots
3. Recommend the most tax-efficient lot(s) to sell

Example output:
```
Lot 1: 100 shares @ $50 (Jan 2024) → LT gain of $3,000, tax: $450
Lot 2: 100 shares @ $70 (Aug 2025) → ST gain of $1,000, tax: $350
Lot 3: 100 shares @ $85 (Nov 2025) → ST loss of ($500), tax savings: $175

Recommendation: Sell Lot 3 first to harvest the loss, then Lot 1 for the lower LT rate.
```

---

## Edge Cases

- **Inherited assets**: Step-up in basis to FMV at date of death
- **Gifted assets**: Donor's basis carries over (for gains); FMV at gift date (for losses)
- **Stock splits**: Adjust cost basis proportionally
- **Reinvested dividends**: Each reinvestment is a separate lot with its own basis and date
- **Cryptocurrency**: Taxed as property; same rules apply but no wash sale rule (as of 2024, changes in 2025)
- **Collectibles**: 28% max rate for long-term gains
- **Section 1202 QSBS**: Potential 50-100% exclusion — flag if user mentions startup stock held 5+ years

---

## Important Disclaimers

Always include at the end:
- This is an estimate for planning purposes, not tax advice
- Actual tax may vary based on complete tax situation
- Consult a tax professional for personalized advice
- Tax rates are based on 2025 brackets and may change

---

## Reference Data

Read `references/tax-rates-2025.md` for current federal and state tax brackets, LTCG thresholds, NIIT thresholds, and other rate details. Always use this file for rate lookups to ensure accuracy.
