# Prompt: Comparison Analysis (Horizontal / Vertical)

Use this to find factors the System Model missed — this is an active search technique, not passive brainstorming. Referenced from `model.md`.

## Horizontal comparison

Find a pair (or set) of peer objects/groups that are similar on every factor already in the model, but whose outcome differs meaningfully. The unexplained gap is evidence of a missing factor.

```
Object/Group A:  <known factors ①②③... match Object B>
Object/Group B:  <known factors ①②③... match Object A>
Outcome A:       <value>
Outcome B:       <value, meaningfully different from A>

-> Since A and B agree on every currently-modeled factor but disagree on outcome,
   list every OTHER difference between A and B:
   - <candidate factor 1>
   - <candidate factor 2>
   - ...
-> Rank candidates by plausibility, carry the top ones into explain.md Step 4.1
```

Example shape (domain-agnostic): comparing two regions/cohorts/app builds/services that are matched on the known drivers but diverge on the metric of interest.

## Vertical comparison

Find the point in time where the outcome changed sharply (regression, breakout, inflection) and inventory everything that changed in the surrounding window.

```
Timeline:
  ... stable baseline ...
  T-1: <state just before the change>
  T:   <the outcome shift happens here>
  T+1: <state just after>

What else changed in the [T-1, T+1] window?
  - <change candidate 1>  (deploy / policy / seasonal / external event / config change)
  - <change candidate 2>
  - ...

-> Rank by temporal proximity to T and mechanistic plausibility,
   carry the top candidates into explain.md Step 4.1
```

## After finding a candidate

A factor found through comparison is still a **surface-level label** at this point (e.g. "housing cost", "a new SDK was added"). Do not add it directly to the Root Cause Tree — send it through the mandatory 5Why drill-down in `explain.md` Step 4.2 first, and tag it `source: comparative discovery (horizontal|vertical)` so its provenance stays traceable in the final report.

## When to re-run this

Re-run comparison analysis whenever `explain.md` Step 4.7 (convergence check) determines explanatory power is still insufficient — a fresh comparison, ideally against the sub-group where the current model fits worst (largest residual), is one of the most reliable ways to surface the next missing factor.
