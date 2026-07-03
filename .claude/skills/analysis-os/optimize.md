# Phase 6 — Optimize

**Goal:** turn the root cause and predictions into a prioritized, actionable plan.

## Evaluate every candidate action against

- **Cost** — engineering time, infra spend, opportunity cost
- **Risk** — what could this action break? (map back to the invariants from Phase 2)
- **ROI** — expected improvement in the Phase 1 metric, relative to cost
- **Complexity** — implementation difficulty, number of systems touched
- **Maintainability** — does this add long-term burden, or reduce it?
- **Scalability** — does the fix hold as load/scope grows, or is it a band-aid?

## Discipline

- Do not propose an action that isn't traceable back to a specific root cause from Phase 4 — "let's also just clean up this unrelated code" is scope creep, not optimization.
- If multiple root causes were found, propose actions per-cause and make trade-offs between them explicit (e.g. "fixing cause A gets 80% of the improvement for 20% of the effort; cause B is the long tail").
- Flag actions that only mitigate a symptom vs. those that address the root cause — both can be valid (e.g. "ship the mitigation now, root-cause fix next sprint"), but the report must be honest about which is which.

## Deliverable: Priority Action Plan

```
Action:          <specific, assignable action>
Addresses:       <which root cause>
Expected impact: <quantified where possible>
Cost/Risk:       <brief>
Priority:        <P0/P1/P2 or similar>
Trade-offs:      <what this action gives up>
```
