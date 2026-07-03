# Graph Model (preview of v2.0)

Even in v1.0, Analysis OS output is written in a graph-friendly shape so migration to a real graph store is low-cost later.

## Node types

| Type | Example |
|---|---|
| Object | `SurfaceFlinger`, `Customer`, `AMS` |
| State | `Cold`, `Warm`, `Idle`, `Busy` |
| Event | `Deploy v2.3.1`, `Config change`, `Traffic spike` |
| Metric | `TTID_p90`, `crash_rate`, `conversion_rate` |
| Constraint | `16ms_frame_budget`, `Q2_budget_cap` |
| Evidence | a single Phase-3 observation row |
| Hypothesis | a single Phase-4 candidate explanation |
| Cause | a Hypothesis promoted to validated status |
| Decision | a single Phase-6 action item |

## Edge types

| Edge | Meaning |
|---|---|
| depends_on | structural/runtime dependency |
| causes | validated causal link |
| changes | an Event changes a State or Metric |
| observes | Evidence observes an Object/Metric/State |
| violates | a State/Event violates a Constraint or Invariant |
| produces | an Object produces an Event or Metric |
| blocks | a Constraint blocks a Decision |
| consumes | an Object consumes a Resource |

## Why this matters

Once analyses are graphs instead of documents, cross-analysis queries become possible: "which past root causes involved Binder contention," "which Decisions never got their expected Metric improvement," "show me every Constraint violated across the last 6 months of incident analyses." That's the entire point of v2.0.
