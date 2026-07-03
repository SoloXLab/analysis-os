# Phase 2 — Model

**Goal:** construct a complete system model. Never analyze data before this phase is complete — data without a model produces correlation-hunting, not understanding.

Build each of the following. Not every category applies to every system, but check all of them explicitly rather than silently skipping.

## Objects
What entities exist in this system? (e.g. Android: AMS, Activity, Process, Binder, CPU, GPU. Business: Customer, Channel, SKU, Campaign.)

## Structure
How are the objects organized? Architecture, module hierarchy, network topology, org structure, pipeline stages, scene graph.

## Processes
How does the system execute over time? Represent as a lifecycle/sequence, e.g.:
```
Fork → Attach → Bind → Create → Resume → Draw
```

## Dependencies
What depends on what? Represent as a directed graph — see `prompts/dependency-graph.md`.

## States
What states can the system (or its key objects) be in? e.g. Cold / Warm / Hot, Idle / Busy / Error.

## Resources
What is consumed? CPU, GPU, disk, battery, memory, bandwidth, money, people-hours.

## Constraints
System limitations: 16ms frame budget, context window, bandwidth caps, budget, API rate limits, power envelope.

## Invariants
Things that must always remain true, and whose violation is itself diagnostic. e.g. "Application created before Activity", "Frame ID must be continuous", "Transaction must be ACID", "Planner loop must terminate".

## Feedback loops
Positive loops (amplifying), negative loops (dampening/stabilizing), control loops (actively correcting toward a setpoint).

## Comparative discovery (finding factors the model missed)

Before treating the object/dependency list above as complete, actively hunt for missing factors using two comparison techniques — do not rely solely on brainstorming from first principles. See `prompts/comparison-analysis.md` for the full template.

**Horizontal comparison** (peer objects/groups at the same time): find two instances that are similar on every factor already in the model, but whose outcome (the Phase 1 metric) differs significantly. The gap is evidence of a missing factor.
```
A and B share the same known factors (layers/objects already modeled),
but their outcomes differ meaningfully
-> there must be an unmodeled factor X explaining the gap
-> enumerate every other difference between A and B to find candidates for X
```

**Vertical comparison** (the same object/system over time): find the point where the outcome changed sharply (a regression, a breakout, a step-change) and inspect what else changed around that same point — new factor candidates live in that window.

Any factor found this way gets folded back into the Objects/Dependencies sections above — tag it with `source: comparative discovery` so its provenance is traceable, and give it the same 5Why treatment described in `explain.md` before accepting it as a real factor rather than a surface-level label.

## Deliverable: System Model

Present as a short structured write-up plus at least one graph/diagram (object graph, dependency graph, or state machine — see `prompts/system-model.md`). A system model without a visual representation is incomplete for anything beyond trivial systems.
