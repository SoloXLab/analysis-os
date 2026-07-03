# Prompt: Timeline

Use a timeline when the analysis target is fundamentally about *when* things happened relative to each other (regression appeared, event sequence during a crash, funnel step timing).

```
T+0ms   <event>          [source: <trace/log>]
T+12ms  <event>
T+45ms  <event>  <-- deviation from baseline starts here
T+160ms <event>          [SLA breached here]
```

For regression analysis specifically, always show:
1. The last known-good timeline/value
2. The first known-bad timeline/value
3. What changed in between (deploys, config changes, traffic shifts, OS/library version bumps)

A timeline without a "what changed in between" section is incomplete for root-causing a regression.
