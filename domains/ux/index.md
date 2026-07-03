# Domain pack: UX / Product

## Key objects
User, session, funnel step, feature flag/experiment, cohort.

## Key metrics
Conversion rate per funnel step, retention (D1/D7/D30), task success rate, time-on-task, NPS/CSAT.

## Common failure modes / root causes
- Funnel drop-off caused by a UI/technical friction point (misattributed to "user doesn't want this" without checking)
- Confounded cohort comparison (e.g. new users vs. power users compared without controlling for tenure)
- Metric improvement from a change that's actually a measurement artifact (tracking bug, sampling change)
- Novelty effect inflating short-term metrics for a UI change that doesn't hold up longer-term

## Diagnostic approach
Before attributing a metric change to a product decision, rule out: tracking/instrumentation changes, population/cohort mix shift, seasonality, and external events — in that order — before accepting a causal product explanation. See `digital-user-research` skill for passive evidence-gathering from reviews/community discussion when direct user research isn't available.
