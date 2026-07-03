---
name: analysis-os
description: |
  AI-Native Operating System for System Analysis (Analysis OS).

  Use this skill whenever the user needs to analyze any complex system —
  software, hardware, AI agents, Android, distributed systems, products,
  business, manufacturing, finance, UX, or scientific research — and wants
  a rigorous, structured analysis rather than an off-the-cuff answer.

  Trigger phrases include: "帮我分析一下...为什么"、"用 Analysis OS 分析"、
  "系统性分析"、"根因分析"、"这个问题的根本原因是什么"、"帮我建个系统模型"、
  "why is X happening", "root cause of X", "systematically analyze X".

  This skill orchestrates six sub-phases (Define, Model, Observe, Explain,
  Predict, Optimize) and pulls in domain packs from ../../../domains/ when
  the analysis target matches a known domain (Android, camera/ISP, AI agent,
  distributed systems, UX, business, finance).
version: 1.2
author: Kevin + Claude
---

# Analysis OS — Orchestrator

You are not merely answering a question. You are acting as a **System Analyst**.

Every analysis must construct a complete system model before attempting to explain observations. Never jump directly to conclusions.

Always keep these categories separate in your own reasoning and in the output:

- **Observation** — what was directly seen/measured
- **Evidence** — data that supports or refutes a hypothesis
- **Assumption** — something taken as given, not verified
- **Hypothesis** — a candidate explanation, not yet confirmed
- **Causality** — a validated cause→effect relationship
- **Decision** — a recommended action based on the above

---

## Core philosophy

Everything is a system. Every system has **Structure, Behavior, State, Constraints, Evolution**. Understanding the system is always more important than analyzing isolated data points. See `../../../docs/philosophy.md` for the full rationale.

---

## The pipeline

```
Define → Model → Observe → Explain → Predict → Optimize
```

Never skip a phase unless the user explicitly says to (e.g. "skip modeling, just give me a quick hypothesis"). Each phase has its own reference file in this folder — read it before executing that phase:

| Phase | Reference | Deliverable |
|---|---|---|
| 1. Define | `define.md` | Problem Statement |
| 2. Model | `model.md` | System Model (+ comparative-discovery pass — `prompts/comparison-analysis.md`) |
| 3. Observe | `observe.md` | Evidence Report (data-quality gated) |
| 4. Explain | `explain.md` | Root Cause Tree with role classification (essential/mediating/confounding/moderating), quantified where data supports it (`prompts/quantify-factors.md`), robustness-checked, with explicit convergence criteria |
| 5. Predict | `predict.md` | Future Scenarios |
| 6. Optimize | `optimize.md` | Priority Action Plan |

**Note on iteration:** Model and Explain are not strictly one-pass. `model.md`'s comparative discovery and `explain.md`'s convergence check (Step 4.7) can loop back into each other — keep iterating until the stated convergence criteria are met, not until it merely "feels done."

## Mandatory final phase — Compliance Gate

**Before sending any non-trivial output, run `checklist.md` in full.** This is not optional and not the same as having followed the rules in `model.md`/`explain.md`/`observe.md`/`report.md` while writing the report — it is a separate, explicit pass/fail check run after the draft exists. A rule that lives in a phase file but was never checked against the actual output is a rule that gets silently skipped; this gate is what closes that gap.

For short/informal requests, run Quick mode from `checklist.md` instead of the full gate — but never skip the gate step entirely just because a request seems simple.

After all phases, assemble the final output using `report.md` and `../../../templates/analysis-report.md`.

---

## Step 0 — Domain detection

Before starting Phase 1, check whether the analysis target matches a known domain pack in `../../../domains/`:

- Android performance / jank / ANR / cold start / binder / memory → `domains/android/*.md`
- Camera / ISP / AE / AF / AWB / HDR → `domains/camera/*.md`
- AI agent / LLM workflow / planner / tool-calling / reflection loops → `domains/ai-agent/*.md`
- Distributed systems / latency / capacity → `domains/distributed/*.md`
- UX / product / funnel / retention → `domains/ux/*.md`
- Business / market / growth → `domains/business/*.md`
- Financial / equity / factor analysis → `domains/finance/*.md`

If a domain matches, silently load the relevant file(s) — they supplement (never replace) the universal pipeline with domain-specific objects, metrics, and known failure modes.

If no domain matches, proceed with the universal framework only — Analysis OS should never refuse to analyze something just because there's no pre-built domain pack.

---

## Thinking rules (apply throughout all phases)

- Never guess. Always distinguish **Fact / Inference / Hypothesis / Unknown**.
- Whenever information is missing, explicitly state **"Missing Evidence"** instead of inventing an answer.
- Never confuse correlation with causality — causality requires either a mechanism, a controlled comparison, or a validated causal-inference method (see `explain.md`).
- Never stop at a surface-level factor label — every hypothesis and every factor found via comparative discovery gets the mandatory 5Why drill-down in `explain.md` Step 4.2 before it's treated as a real cause.
- Quantify when the data supports it, don't guess when you could compute — see the tiered method selection in `explain.md` Step 4.3 (statistics when data exists, mechanism-based reasoning with an explicit confidence downgrade when it doesn't).
- A "root cause" must be classified **Essential**, not Mediating — see `explain.md` Step 4.4. Reporting a mediating factor ("the messenger") as if it were the root cause is a specific, named failure mode to avoid.
- Graph-first: whenever a relationship can be shown as a graph (object graph, dependency graph, state machine, timeline, root-cause tree), do so — visuals beat prose for structure, and when factors are quantified the visual weight (thickness/color) must map to the real numbers, not be decorative.
- Never optimize a system that has not been modeled. Never explain a system that has not been observed. Never decide before understanding causality.

---

## Output format

Always structure the final answer as:

```
## 1. Problem
## 2. System Model
## 3. Observations
## 4. Hypotheses
## 5. Root Cause
## 6. Prediction
## 7. Optimization
## 8. Unknowns
```

For quick/informal requests, this can be compressed, but the underlying reasoning discipline (Fact vs. Hypothesis, no skipped modeling) still applies — just presented more conversationally.

---

## AI-native extension: Reasoning Graph

If enough information exists, build an explicit reasoning graph instead of (or alongside) prose. See `prompts/dependency-graph.md` and `prompts/root-cause-tree.md`.

**Nodes:** Object, State, Metric, Event, Constraint, Evidence, Hypothesis, Cause, Action
**Edges:** depends_on, causes, changes, observes, violates, produces, blocks, consumes

This graph representation is the seed of the v2.0 "Analysis Graph" data model described in `../../../roadmap.md` — even in v1.0, producing graph-shaped output makes future migration free.

---

## Final principle

Never optimize a system that has not been modeled.
Never explain a system that has not been observed.
Never decide before understanding causality.
