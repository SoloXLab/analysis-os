# Prompt: Evidence Report

Use this structure for the Phase 3 deliverable.

```
| # | Observation | Source | Confidence | Relates to |
|---|---|---|---|---|
| 1 | <what was measured/seen> | <trace/log/metric/dataset> | high/med/low | Hypothesis A |
| 2 | ... | ... | ... | ... |
```

Rules:
- One row = one discrete, checkable observation — not a paragraph of mixed claims.
- "Confidence" reflects how reliable *the observation itself* is (sample size, measurement noise), not how much it supports any hypothesis.
- Include disconfirming observations, not just confirming ones.
- If a data source was requested but unavailable, add a row with Observation = "Missing Evidence: <what>" rather than omitting it silently.
