---
name: etf-tax-efficiency-scorer
description: Compare and score ETFs by tax efficiency to help investors choose the most tax-friendly funds for taxable accounts. Use this skill when someone asks "which ETF is more tax efficient", "best ETFs for taxable account", "tax-efficient investing", "compare ETFs for taxes", "which fund distributes less in capital gains", "tax-friendly index funds", or any question about choosing investments based on tax impact. Also trigger when users ask about asset location (which funds go in which account type), dividend tax treatment, or want to understand why some funds generate more taxable events than others. Covers ETFs, mutual funds, and index funds.
---

# ETF Tax Efficiency Scorer

## Purpose

Not all index funds are created equal from a tax perspective. Two funds tracking the same index can have dramatically different tax costs in a taxable account. This skill scores and compares funds on tax efficiency so investors can make informed choices about which funds belong in taxable accounts vs. tax-advantaged accounts.

The difference matters: a tax-inefficient fund in a taxable account can cost 0.5-1.5% per year in unnecessary taxes compared to a tax-efficient alternative providing identical market exposure.

---

## Tax Efficiency Scoring Framework

### Score Components (0-100 scale)

Each fund gets a composite tax efficiency score based on these factors:

#### 1. Structure Score (0-25 points)
```
ETF:                    25 points (in-kind creation/redemption avoids cap gains)
Index Mutual Fund:      15 points (less efficient redemption mechanism)
Active Mutual Fund:      5 points (frequent trading generates distributions)
Closed-End Fund:        10 points (no redemptions but may trade at discount)
```

Why: ETFs have a structural advantage — authorized participants can redeem shares "in-kind" (exchanging ETF shares for the underlying stocks), which purges low-basis shares without triggering taxable events for remaining holders.

#### 2. Turnover Score (0-20 points)
```
Turnover < 5%:          20 points
Turnover 5-15%:         15 points
Turnover 15-30%:        10 points
Turnover 30-50%:         5 points
Turnover > 50%:          0 points
```

Why: Every time a fund sells a holding at a gain, it must distribute that gain to shareholders. Lower turnover = fewer forced taxable events.

#### 3. Distribution History Score (0-25 points)
```
No capital gains distributed (3yr):     25 points
Minimal CG distributions (<0.5%/yr):    20 points
Small CG distributions (0.5-2%/yr):     10 points
Significant CG distributions (>2%/yr):   0 points
```

Why: Past distributions are the best predictor of future distributions. Check the fund's actual distribution history, not just its strategy.

#### 4. Dividend Tax Treatment Score (0-15 points)
```
No/minimal dividends (growth stocks):       15 points
Mostly qualified dividends (US equities):    12 points
Mix of qualified/non-qualified:               8 points
Mostly non-qualified (bonds, REITs, intl):    3 points
All ordinary income (bond funds):             0 points
```

Why: Qualified dividends are taxed at LTCG rates (0/15/20%), while non-qualified dividends and bond interest are taxed at ordinary income rates (up to 37% + state).

#### 5. Dividend Yield Impact (0-15 points)
```
Yield < 0.5%:     15 points
Yield 0.5-1.5%:   12 points
Yield 1.5-2.5%:    8 points
Yield 2.5-4%:      4 points
Yield > 4%:        0 points
```

Why: Higher yields mean more annual taxable income, regardless of qualification status. Growth-oriented funds that retain earnings are more tax-efficient in taxable accounts.

---

## Common Fund Comparisons

When users ask for ETF comparisons, here are reference scores for popular categories:

### US Broad Market (Most Tax-Efficient Category)
| Fund | Type | Expense | Yield | Turnover | Tax Score | Notes |
|---|---|---|---|---|---|---|
| VTI | ETF | 0.03% | ~1.3% | 4% | 90+ | Gold standard |
| ITOT | ETF | 0.03% | ~1.3% | 4% | 90+ | iShares equivalent |
| SCHB | ETF | 0.03% | ~1.3% | 4% | 90+ | Schwab equivalent |
| SPTM | ETF | 0.03% | ~1.3% | 4% | 90+ | SPDR equivalent |
| VTSAX | MF | 0.04% | ~1.3% | 4% | 80 | Mutual fund version |

### S&P 500
| Fund | Type | Expense | Yield | Turnover | Tax Score | Notes |
|---|---|---|---|---|---|---|
| VOO | ETF | 0.03% | ~1.3% | 2% | 92+ | Lowest turnover |
| IVV | ETF | 0.03% | ~1.3% | 2% | 92+ | iShares equivalent |
| SPY | ETF | 0.09% | ~1.3% | 2% | 88 | Unit trust structure, less efficient |
| SPLG | ETF | 0.02% | ~1.3% | 2% | 92+ | Cheapest |

### Growth (Very Tax-Efficient)
| Fund | Type | Expense | Yield | Turnover | Tax Score | Notes |
|---|---|---|---|---|---|---|
| VUG | ETF | 0.04% | ~0.5% | 5% | 92+ | Low yield = low annual tax |
| QQQ | ETF | 0.20% | ~0.6% | 8% | 88 | Higher expense, Nasdaq 100 |
| SCHG | ETF | 0.04% | ~0.4% | 5% | 93+ | Very low yield |
| IWF | ETF | 0.19% | ~0.6% | 15% | 82 | Higher turnover |

### International (Less Tax-Efficient)
| Fund | Type | Expense | Yield | Turnover | Tax Score | Notes |
|---|---|---|---|---|---|---|
| VXUS | ETF | 0.07% | ~3.0% | 4% | 65 | High yield, foreign tax drag |
| IXUS | ETF | 0.07% | ~2.8% | 4% | 67 | Similar to VXUS |
| EFA | ETF | 0.32% | ~2.8% | 5% | 58 | Higher expense |

### Bonds (Least Tax-Efficient)
| Fund | Type | Expense | Yield | Turnover | Tax Score | Notes |
|---|---|---|---|---|---|---|
| BND | ETF | 0.03% | ~3.5% | 40% | 25 | All ordinary income |
| AGG | ETF | 0.03% | ~3.5% | 40% | 25 | Similar to BND |
| MUB | ETF | 0.07% | ~2.5% | 10% | 75 | Federal tax-exempt! |
| VTEB | ETF | 0.05% | ~2.5% | 10% | 78 | Federal tax-exempt |
| CMF | ETF | 0.07% | ~2.0% | 10% | 85 | CA state + fed exempt |

### REITs (Tax-Inefficient)
| Fund | Type | Expense | Yield | Turnover | Tax Score | Notes |
|---|---|---|---|---|---|---|
| VNQ | ETF | 0.12% | ~3.8% | 6% | 20 | Most dividends = ordinary income |
| SCHH | ETF | 0.07% | ~3.5% | 5% | 22 | Slightly better |

---

## Asset Location Recommendations

Based on tax efficiency scores, recommend where each fund type belongs:

### Taxable Account (Best for tax-efficient funds)
```
BEST FIT:
- US total market ETFs (VTI, ITOT, SCHB)
- S&P 500 ETFs (VOO, IVV, SPLG)
- US growth ETFs (VUG, SCHG, QQQ)
- Municipal bond ETFs (MUB, VTEB, state-specific like CMF)
- Tax-managed funds (VTCLX, VTMFX)

REASON: These generate minimal taxable events; munis are tax-exempt
```

### Tax-Advantaged Account — IRA/401(k) (Best for tax-inefficient funds)
```
BEST FIT:
- Bond funds (BND, AGG, BNDX)
- REIT funds (VNQ, SCHH)
- High-dividend value funds (VTV, VYM)
- International funds (VXUS, IXUS) — though foreign tax credit argument exists
- Actively managed funds with high turnover
- TIPS funds (VTIP, SCHP)

REASON: Dividends and interest compound tax-free; no annual tax drag
```

### Special Case: International Funds
```
International funds have a nuance:
- In TAXABLE: You get a foreign tax credit for taxes withheld by foreign governments
- In IRA/401(k): Foreign taxes are withheld but you get NO credit (lost forever)
- RECOMMENDATION: If portfolio is large enough to claim FTC, hold international in taxable
  Otherwise, the high dividend yield argues for tax-advantaged
```

---

## Output Format

### Single Fund Analysis
```
[TICKER] — [Fund Name]
━━━━━━━━━━━━━━━━━━━━━━━
Tax Efficiency Score: XX/100

Structure:          XX/25  [ETF/MF/Active]
Turnover:           XX/20  [X% annual]
Distribution Hx:    XX/25  [CG distributions past 3yr]
Dividend Quality:   XX/15  [% qualified]
Dividend Yield:     XX/15  [X.X% yield]

Recommended Account: [Taxable / Tax-Advantaged / Either]
Annual Tax Cost Estimate: ~$XXX per $10,000 invested
  (at [Federal Rate]% + [State Rate]% marginal rates)
```

### Comparison Table
```
COMPARISON: Taxable Account Tax Impact

                    [FUND A]    [FUND B]    [FUND C]
Tax Score:          XX/100      XX/100      XX/100
Expense Ratio:      X.XX%       X.XX%       X.XX%
Dividend Yield:     X.X%        X.X%        X.X%
Qualified %:        XX%         XX%         XX%
Turnover:           XX%         XX%         XX%
Recent CG Dist:     $X.XX       $X.XX       $X.XX

Est. Annual Tax/$10K:
  Federal:          $XXX        $XXX        $XXX
  State ([ST]):     $XXX        $XXX        $XXX
  Total:            $XXX        $XXX        $XXX

RECOMMENDATION: [Fund X] is the most tax-efficient choice for a taxable account,
saving approximately $XXX/year per $10,000 vs [Fund Y].
```

---

## Data Sources

When analyzing specific funds, use available knowledge about:
- Expense ratios
- Historical dividend yields
- Turnover rates
- Capital gains distribution history
- Fund structure (ETF vs mutual fund vs unit trust)
- Qualifying dividend percentages

If the user needs real-time data, suggest checking:
- Morningstar (tax cost ratio)
- Fund provider websites (distribution history)
- ETF.com (fund comparison tools)

---

## Important Notes

- Tax efficiency scores are estimates based on fund characteristics and historical behavior
- Past distribution history doesn't guarantee future distributions
- A fund's tax efficiency is just one factor — expense ratios, tracking error, and total return also matter
- The "best" fund depends on which account it goes in; a tax-inefficient fund in an IRA has zero tax drag
- Municipal bond yields should be compared on a tax-equivalent basis: Tax-Equiv Yield = Muni Yield / (1 - Marginal Tax Rate)

---

## Reference Data

Read `references/tax-rates-2025.md` for current tax rates to calculate annual tax cost estimates.
