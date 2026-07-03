# Phase 4 — Explain

**Goal:** build explanations from evidence. Never confuse correlation with causality — and never stop at a surface-level factor label when a deeper, more actionable root cause is one "why" away.

## Step 4.1 — Generate hypotheses

Generate multiple candidate hypotheses — resist anchoring on the first plausible one. Include hypotheses surfaced by the comparative discovery step in `model.md`, not just ones generated from first-principles brainstorming.

## Step 4.2 — Mandatory recursive drill-down (5Why) on every hypothesis

**This step is mandatory, not optional** — do not stop at a hypothesis's first stated form.

For every hypothesis/candidate cause, recursively ask "why" until one of these stop conditions is met:
- it reaches a policy/mechanism/physical constant that cannot be decomposed further
- two consecutive answers repeat the same explanation (circular)
- the next level is too fine-grained to be measurable or actionable (back off one level)
- 5 levels reached without hitting a natural stop

```
Hypothesis: <surface-level factor>
  Why-1: why does this happen?        -> <factor 1 level deeper>
  Why-2: why does that happen?        -> <factor 2 levels deeper>
  Why-3: ...                          -> ...
  -> stop when a hard-to-decompose root is reached
```

Do this for **every** hypothesis, including ones found via comparative discovery — a factor found by comparison ("housing cost", "cultural attitude") is still just a surface label until it's been through this same drill-down. Record the parent→child chain explicitly; it feeds both the factor-role classification below and the visualization in `report.md`.

## Step 4.3 — Quantify where data supports it (graceful degradation)

Rank the evidence-gathering method available for this specific analysis, and use the strongest one the data actually supports — don't skip straight to qualitative reasoning if quantification is possible.

```
Tier A - sample data available (n > ~30), cross-sectional or panel:
  -> single-variable correlation (r) per candidate factor
  -> multivariate regression -> standardized beta (β) per factor
  -> compression rate = (|r| - |β|) / |r| x 100%
     compression < 40%  -> essential factor candidate (independent contribution)
     compression 40-70% -> mediating factor candidate (mostly relayed through another factor)
     compression > 70%  -> proxy/confounding variable (effect mostly disappears once controlled)
  -> VIF > 10 between two factors -> flag collinearity, keep the theoretically more fundamental one

Tier B - time series available:
  -> Granger-style lead-lag test (does X's past predict Y's future beyond Y's own history?)
  -> note explicitly: Granger causality is predictive, not proof of true causality

Tier C - natural experiment / policy break available:
  -> difference-in-differences or regression discontinuity around the break point

Tier D - no usable data:
  -> logical/mechanism-based reasoning + cited precedent
  -> explicitly label the conclusion "causal relationship based on theoretical
     reasoning, not empirically validated" — do not present it with the same
     confidence as a Tier A/B/C finding
```

Never silently drop to Tier D language ("X causes Y") when only a Tier D method was actually used. The tier used should be visible in the final report next to each hypothesis.

See `prompts/quantify-factors.md` for the statistical templates and a reusable Python snippet for Tier A.

## Step 4.4 — Classify factor role (not just rank)

Once a hypothesis has evidence (qualitative or quantitative), classify its **role**, not just its confidence:

| Role | Meaning | How to recognize it |
|---|---|---|
| **Essential (本质)** | independent causal contribution, survives multivariate control | compression < 40% (Tier A), or: removing it changes the outcome even with all other known factors held constant (qualitative) |
| **Mediating (中介)** | real effect, but it's a relay for a deeper factor | compression 40–70%, or: the 5Why drill-down in Step 4.2 found a deeper factor that fully explains it |
| **Confounding (混淆)** | correlates with the real cause but has little independent effect | compression > 70%, or: disappears once the true driver is held constant |
| **Moderating (调节)** | doesn't drive the outcome by itself, but changes how strongly another factor matters | effect only appears as an interaction/cross-term, or is only observed in a subset of cases |

A "root cause" in the final report should be an **Essential** factor at the deepest level its 5Why chain reached — not a Mediating factor that merely sits between the real driver and the symptom. Reporting a Mediating factor as "the root cause" is a common failure mode this classification exists to prevent.

## Step 4.5 — Robustness / cross-group validation

Before finalizing a factor's role, check whether its effect is stable:

- **Cross-group**: does the same factor's effect (β, or qualitative strength) hold across different sub-populations / regions / time periods / segments? If it swings by more than roughly half its magnitude across groups, downgrade it to **conditional** rather than treating it as universally essential — different regimes can have entirely different dominant factors (e.g. the dominant driver in a high-value regime is often not the dominant driver in a low-value regime).
- **Perturbation**: does removing outliers or changing the time granularity change the conclusion by more than ~20%? If yes, flag as fragile.

## Step 4.6 — Reject inconsistent hypotheses

A hypothesis that contradicts even one solid observation should be down-weighted or dropped, not quietly ignored. Where a hypothesis cannot be confirmed or rejected with available evidence, say so explicitly (`Unknown`) rather than defaulting to "probably true."

## Step 4.7 — Convergence check (when to stop iterating)

Explain is not always a single pass. Loop back to Step 4.1 / to `model.md`'s comparative discovery when **any** of these hold:
- a Tier A model's R² (or equivalent explanatory power) is still low relative to the Phase 1 target
- a factor was classified Mediating but its parent (deeper) factor hasn't been identified yet
- residual/unexplained variance shows a systematic pattern (not noise) — that pattern points to a missing factor
- cross-group validation (Step 4.5) found a sub-group where the current explanation clearly doesn't hold

Stop iterating when:
- additional iterations improve explanatory power by less than a small margin (e.g. R² gain < 0.05 in a Tier A setting), or the qualitative equivalent: a new round of comparative discovery surfaces no new candidate factors
- every retained factor has a defensible role classification (Step 4.4) and, where quantified, is statistically significant
- the user confirms the explanation is sufficient for the stated Phase 1 target

Don't iterate indefinitely by default — state the convergence reasoning explicitly so the person reading the report knows why the analysis stopped where it did.

## Deliverable: Root Cause Tree

```
Root Cause(s):        <ranked list, Essential-role factors at their deepest 5Why level>
Role:                 <Essential / Mediating / Confounding / Moderating, per factor>
Evidence tier:        <A/B/C/D, per factor>
Quantification:       <r / β / compression, if Tier A>
Confidence:           <per cause>
Robustness:           <stable / conditional — per Step 4.5>
Supporting evidence:  <per cause>
Contradicting evidence: <per cause, if any>
Unknowns:             <what would need to be true / measured to increase confidence>
```

Prefer a visual root-cause tree or fishbone diagram over prose when there are 3+ candidate causes — see `prompts/root-cause-tree.md`. When factors are quantified, the diagram's visual weight (line thickness, etc.) should map to the actual β/effect size, not be uniform — see the visualization rules in `report.md`.
