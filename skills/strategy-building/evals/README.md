# Evals for `strategy-building`

Eval-driven iteration loop for this skill, following https://agentskills.io/skill-creation/evaluating-skills.

## Files

- `evals.json` — the test cases you author by hand. Prompt + expected_output now; add `assertions` after the first run.
- `files/` — input files referenced by test cases (none yet — this skill is text-only).

Eval *results* live in a sibling workspace directory, not here:

```
retail-skills-us/
  skills/strategy-building/
    SKILL.md
    evals/
      evals.json
      README.md
  strategy-building-workspace/        <-- gitignored, created on first run
    iteration-1/
      eval-fuzzy-roth-growth/
        with_skill/{outputs,timing.json,grading.json}
        without_skill/{outputs,timing.json,grading.json}
      ...
      benchmark.json
```

## The loop

1. **Run each case twice** — once with `SKILL.md` loaded, once without. Spawn each run in a fresh subagent / clean session so there is no leakage from skill development.
2. **Read the outputs** before writing assertions. You do not yet know which rules baseline Claude follows for free.
3. **Add `assertions` to each case** — concrete, observable, countable. See "Assertion ideas" below.
4. **Grade** each run against its assertions, recording PASS/FAIL with evidence (a quote or file reference, not an opinion).
5. **Aggregate** into `iteration-N/benchmark.json`. The interesting number is the **delta** between with_skill and without_skill — pass-rate lift, plus token / time cost.
6. **Drop assertions that pass in both configs** — they are noise. Keep the ones the skill is uniquely responsible for.
7. **Iterate** SKILL.md, then run iteration-2 in a new directory. Repeat until improvement plateaus.

## Assertion ideas (add after iteration-1)

These are the rules SKILL.md explicitly enforces — baseline Claude is unlikely to produce all of them unprompted.

### Both branches

- The response asks the user clarifying questions before producing a spec, OR explicitly flags which Required interview items are being assumed.
- The final spec contains every section from the matching template, including `Open Questions`.
- Entry, Sizing, Rebalance, Contributions, and Exit / Review are each answered with a concrete mechanical rule (no placeholders, no "depends on your situation").
- Asset location respects the account type (e.g., bonds / REITs preferred in tax-advantaged accounts when both exist).
- The output does not endorse or validate any specific stock pick as a "good trade".
- The spec includes an educational-framework / not-personal-advice disclaimer.

### Branch B (thesis basket) — these are where the skill earns its keep

- Every ticker has BOTH a one-sentence thesis AND a written invalidation trigger. (No ticker is in the spec without both.)
- The spec names sector or shared demand-driver overlap explicitly, even if the user accepted the concentration.
- The basket is assigned a portfolio role (core / satellite / lottery) with an explicit % cap.
- A max single-name cap is set inside the basket.
- If the user has no surrounding core portfolio, the skill stops and runs Branch A first instead of letting the basket *be* the portfolio.

### Hybrid case

- The existing single-stock position is treated as a separate satellite sub-strategy, not merged into the core allocation.
- RSU / employer-stock concentration risk is flagged.

## Grading the interview vs. grading the spec

This skill is interview-driven, so single-turn evals can only judge the *opener*. Two options:

- **Single-turn (start here)**: assert the response asks the right questions. Cheap, catches most regressions.
- **Scripted multi-turn (add later if needed)**: pre-write user answers to the interview, feed them turn-by-turn, then grade the final spec. More setup, but it actually tests the spec output.

Start single-turn. Only add multi-turn evals if single-turn stops catching meaningful regressions.
