# Phase 4 — Explain

**Goal:** build explanations from evidence. Never confuse correlation with causality.

## Methods (pick what fits the problem)

- **5 Why** — recursively ask why until reaching a controllable root cause, not just a deeper symptom
- **Fishbone / Ishikawa diagram** — organize candidate causes into families (e.g. 人机料法环 / People-Machine-Material-Method-Environment, or domain-specific categories)
- **Fault Tree Analysis** — top-down decomposition of a failure into necessary/sufficient sub-conditions
- **DAG / causal graph** — explicit directed acyclic graph of hypothesized causal relationships
- **Granger causality / lead-lag** — for time series, does X's past predict Y's future beyond Y's own past?
- **Counterfactual reasoning** — "if X had not happened, would Y still have occurred?"
- **Bayesian reasoning** — update hypothesis probabilities as evidence arrives, rather than binary accept/reject

## Process

1. **Generate** multiple candidate hypotheses — resist anchoring on the first plausible one.
2. **Rank** them by how well they're supported by the Phase 3 evidence.
3. **Find evidence for each** — actively look for evidence, don't just reuse what happened to be in Phase 3.
4. **Reject inconsistent hypotheses** — a hypothesis that contradicts even one solid observation should be down-weighted or dropped, not quietly ignored.
5. Where a hypothesis cannot be confirmed or rejected with available evidence, say so explicitly (`Unknown`).

## Deliverable: Root Cause Tree

```
Root Cause(s):     <ranked list>
Confidence:        <per cause>
Supporting evidence: <per cause>
Contradicting evidence: <per cause, if any>
Unknowns:          <what would need to be true / measured to increase confidence>
```

Prefer a visual root-cause tree or fishbone diagram over prose when there are 3+ candidate causes — see `prompts/root-cause-tree.md`.
