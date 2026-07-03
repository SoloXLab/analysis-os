# Architecture

## v1.0 — Skill-based framework (current)

```
analysis-os.md (orchestrator, in .claude/skills/analysis-os/SKILL.md)
    |
    +-- define.md / model.md / observe.md / explain.md / predict.md / optimize.md
    +-- prompts/ (reusable output templates for graphs/tables)
    +-- domains/ (swappable domain knowledge packs)
    +-- templates/ (final report skeletons)
```

Single agent (Claude, or any LLM-based coding/chat agent), sequential phase execution, human-in-the-loop between phases for long analyses.

## v2.0 — Analysis Graph

Introduces a persistent, queryable graph data model underlying every analysis:

```
Node types: Object, State, Event, Metric, Constraint, Evidence, Hypothesis, Cause, Decision
Edge types: depends_on, causes, changes, observes, violates, produces, blocks, consumes
```

This turns each analysis from a one-off document into a structured graph that can be diffed across time, queried, and reused across related analyses (e.g. "show me every past root cause tagged 'Binder contention'").

## v3.0 — Multi-agent Analysis OS

```
                    Analysis Orchestrator
                            |
      +----------+----------+----------+
      v          v                     v
 Define Agent  Model Agent      Evidence Agent
                                        |
                          +-------------+-------------+
                          v                           v
                    Trace Agent                 Log Agent
                          |                           |
                          +-------------+-------------+
                                        v
                              Hypothesis Agent
                                        |
                                        v
                              Causality Agent
                                        |
                                        v
                              Prediction Agent
                                        |
                                        v
                              Optimization Agent
                                        |
                                        v
                               Report Agent
```

All agents read/write the same Analysis Graph, so parallel sub-agents (e.g. Trace Agent + Log Agent running concurrently under Evidence Agent) merge cleanly instead of producing conflicting narratives.

See `roadmap.md` in the repo root for milestones.
