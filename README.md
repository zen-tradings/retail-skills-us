# Retail Investor Skill Suite (US)

A collection of 5 Claude skills designed to help US-based retail investors build strategies, minimize taxes, and make smarter investment decisions.

## Skills Included

### 1. Strategy Building (`skills/strategy-building/`)
**Turn a vague investment goal into an executable spec.**
- Interviews the user to extract goal, horizon, capital, account type, and risk tolerance
- Maps the goal to an archetype (growth, income, preservation, balanced, thematic)
- Produces a written spec with explicit entry, sizing, rebalance, and exit rules
- Names guardrails and open questions up front, before real money moves
- Hands off to the tax skills below for tax-aware execution

### 2. Capital Gains Tax Estimator (`skills/capital-gains-estimator/`)
**Know your tax bill before you sell.**
- Calculates federal + state + NIIT taxes on any potential sale
- Compares short-term vs long-term tax impact
- Shows break-even analysis for holding vs selling
- Handles multi-lot positions and specific identification
- Covers all 50 states

### 3. Tax Loss Harvesting Tracker (`skills/tax-loss-harvesting-tracker/`)
**Turn market losses into tax savings.**
- Scans portfolio for unrealized losses to harvest
- Matches losses to gains using IRS ordering rules
- Suggests wash-sale-safe replacement securities
- Tracks cross-account wash sale risks (taxable, IRA, 401k, spouse)
- Generates step-by-step action plans with calendar reminders

### 4. ETF Tax Efficiency Scorer (`skills/etf-tax-efficiency-scorer/`)
**Choose the right fund for the right account.**
- Scores funds 0-100 on tax efficiency
- Compares funds by structure, turnover, distributions, yield, and dividend quality
- Provides asset location recommendations (taxable vs tax-advantaged)
- Covers ETFs, mutual funds, and municipal bonds
- Includes common swap pairs for tax loss harvesting

### 5. Portfolio Rebalance Tax Calculator (`skills/portfolio-rebalance-tax-calc/`)
**Rebalance without getting clobbered by taxes.**
- Compares naive vs tax-optimized rebalancing approaches
- Prioritizes zero-tax methods (contributions, IRA rebalancing, DRIP redirect)
- Optimizes tax lot selection for minimum tax cost
- Generates phased transition plans for major allocation changes
- Handles multi-account portfolios

## Reference Data

Every tax skill bundles its own `references/tax-rates-2025.md` containing:
- 2025 federal income tax brackets (all filing statuses)
- Long-term capital gains rate thresholds
- Net Investment Income Tax (NIIT) thresholds
- State income tax top marginal rates for all 50 states
- California detailed brackets
- Key tax rules (wash sales, loss limitations, holding periods, qualified dividends)

Each skill is self-contained — you can copy any individual skill folder into `~/.claude/skills/` and it will work without any other files from this repo.

**Sourcing and verification:**
- Federal brackets, LTCG thresholds, NIIT, and standard deductions are taken from IRS Rev. Proc. 2024-40 (the IRS inflation adjustments for tax year 2025)
- State top marginal rates are from each state's department of revenue; double-check before relying on high-income edge cases (e.g., California's 1% Mental Health Services Tax on income > $1M is **not** included in the 13.3% top rate)
- Washington state LTCG threshold is inflation-adjusted annually per RCW 82.87.020 — verify against the current WA DOR notice

**Update this file annually** when new IRS brackets are released (typically in October–November for the following tax year via a new Rev. Proc.). Because each skill bundles its own copy, updates need to be applied to all five skills — keep them in sync.

## Installation

Copy any skill directory (e.g., `skills/strategy-building/`) into your Claude skills folder at `~/.claude/skills/` (personal, all projects) or `.claude/skills/` (a specific project). Each skill is fully self-contained.

Each skill can be used independently, but they work best together — for example, `strategy-building` produces a spec that `portfolio-rebalance-tax-calc` can execute tax-efficiently, and `tax-loss-harvesting-tracker` can identify loss opportunities within a rebalance.

## Who This Is For

- US-based individual investors
- Any filing status (Single, MFJ, MFS, HoH)
- Any state (includes all 50 states + DC)
- Taxable brokerage accounts, IRAs, 401(k)s, HSAs, and multi-account portfolios
- Beginner to advanced investors

## Disclaimer

These skills provide estimates and frameworks for educational and planning purposes only. They do not constitute tax, legal, or investment advice. Tax and regulatory situations vary by individual and change over time; consult a qualified tax professional or fiduciary advisor for personalized guidance before acting on any output from these skills.
