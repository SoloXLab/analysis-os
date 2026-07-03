# Phase 5 — Predict

**Goal:** predict future behavior of the system given the root cause(s) established in Phase 4.

## Methods (pick what fits)

- **Simulation** — run the modeled system forward under assumed conditions
- **Forecast** — time-series extrapolation (with explicit uncertainty bands, not a single point estimate)
- **Digital twin** — a parameterized model that can be queried "what happens if X changes?"
- **Sensitivity analysis** — which input(s) does the outcome depend on most? (rank by elasticity)
- **Scenario planning** — best case / base case / worst case, each with its own trigger conditions
- **Monte Carlo** — for outcomes with meaningful randomness, simulate a distribution rather than a single number
- **Risk analysis** — probability × impact for each identified risk

## Discipline

- Every prediction needs a stated confidence interval or qualitative confidence level — a bare point estimate implies false precision.
- State the assumptions the prediction depends on explicitly; if those assumptions break, say what happens to the prediction.
- If the system has feedback loops (from Phase 2), account for them — linear extrapolation of a system with a strong negative feedback loop will be wrong.

## Deliverable: Future Scenarios

```
Scenario:       <best / base / worst, or named scenario>
Trigger:        <what causes this scenario>
Prediction:     <quantified where possible>
Confidence:     <level + what would falsify it>
```
