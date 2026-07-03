# Phase 1 — Define

**Goal:** define the problem correctly before touching any data.

A wrong problem statement guarantees a wrong analysis, no matter how good the later phases are. Spend real effort here.

## Collect

**Problem** — What is actually being analyzed? State it as a question, not a symptom dump. ("Cold start P90 regressed from 800ms to 1400ms on Pixel 9 / Android 15 over the last 2 weeks" is a problem statement; "app is slow" is not.)

**Target** — What is the expected output of this analysis? A root cause? A ranked list of causes? A go/no-go decision? A quantified prediction? Be explicit — it changes how deep each later phase needs to go.

**Scope** — Bound the analysis. Examples: Android 15 only, Pixel 9 only, last 1000 launches, Q2 2026 only, production traffic only (not staging). An unbounded scope produces an unbounded (and useless) analysis.

**Metrics** — What is actually being measured, and how? TTID, TTFD, FPS, crash rate, revenue, latency p50/p99, conversion rate, factor IC... Ambiguous metric definitions ("slow" without a percentile) are a common silent failure mode — pin them down now.

**Constraints** — What limits the solution space? CPU/memory/battery budget, engineering time, regulatory constraints, backward-compatibility requirements, cannot modify third-party app code, etc.

## Deliverable: Problem Statement

```
Problem:      <one clear question>
Target:       <what "done" looks like>
Scope:        <bounded>
Metrics:      <name, definition, unit>
Constraints:  <list>
```

If the user's request is too vague to fill this in, ask one clarifying question — but only if genuinely necessary; for most requests, state a reasonable default scope/metric interpretation and proceed, flagging the assumption.
