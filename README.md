# Analysis OS

**An AI-Native Operating System for System Analysis and Root Cause Reasoning.**

Analysis OS is not a prompt collection. It is a reusable analytical methodology, expressed as a set of composable Skills, that turns any AI agent (Claude Code, OpenCode, Cursor, Codex, Gemini CLI, LangGraph, OpenAI Agents SDK, MCP...) into a disciplined **System Analyst** rather than a pattern-matching answer generator.

The core belief: **you cannot optimize a system you have not modeled, and you cannot explain a system you have not observed.**

---

## Why

Most AI-assisted analysis jumps straight from "here's some data" to "here's my conclusion." That produces plausible-sounding but shallow answers, because the model never built an explicit model of the system it's reasoning about, never separated fact from inference, and never distinguished correlation from causality.

Analysis OS forces a fixed pipeline instead:

```
Define → Model → Observe → Explain → Predict → Optimize
```

Every phase has a deliverable. No phase can be skipped unless the user explicitly says so. Every claim in the output is tagged as **Fact / Inference / Hypothesis / Unknown** — never invented.

---

## Who this is for

Anyone who needs to analyze a complex system and wants the AI to reason like an analyst, not a chatbot:

- Android / mobile performance engineers (jank, ANR, cold start, memory)
- Camera / ISP engineers (AE/AF/AWB/HDR pipelines)
- AI agent / LLM system builders (planner loops, tool-calling failures)
- Distributed systems / SRE (latency, capacity, cascading failures)
- Product, UX, and business analysts (funnel drop-off, retention, market entry)
- Quant / fundamental investors (factor analysis, causal drivers of a metric)

The **domain knowledge changes**; the **reasoning framework stays constant**.

---

## Repository structure

```
analysis-os/
├── .claude/skills/analysis-os/   # The actual Claude Code Skill (orchestrator + sub-phases + compliance gate)
├── docs/                         # Philosophy, methodology, architecture, graph model
├── domains/                      # Domain packs: android, camera, ai-agent, distributed, ux, business, finance
├── templates/                    # Reusable output templates (report, hypothesis, root-cause, decision...)
├── examples/                     # Worked examples end-to-end
├── diagrams/                     # Visual references for the analysis loop / reasoning graph
└── roadmap.md                    # v1 → v2 (Analysis Graph) → v3 (Multi-Agent) plan
```

---

## Quick start (Claude Code)

1. Copy `.claude/skills/analysis-os/` into your project's `.claude/skills/` directory (or symlink it).
2. Optionally copy the relevant file(s) from `domains/` for your field into the same skills folder, or just reference them — the orchestrator will pull in domain knowledge as needed.
3. Ask Claude to analyze something: *"用 Analysis OS 帮我分析一下 Android 冷启动为什么变慢了"* / *"Use Analysis OS to figure out why our funnel conversion dropped."*
4. Claude will walk Define → Model → Observe → Explain → Predict → Optimize and produce a structured report using `templates/analysis-report.md`.

---

## Core philosophy

Everything is a system. Every system has **Structure, Behavior, State, Constraints, Evolution**. See [`docs/philosophy.md`](docs/philosophy.md) and [`docs/methodology.md`](docs/methodology.md) for the full reasoning behind the pipeline.

## Roadmap

- **v1.0 — Analysis Framework** (this repo, current): universal loop, system modeling, root cause analysis, report templates.
- **v2.0 — Analysis Graph**: a unified data model (Object / State / Event / Metric / Constraint / Evidence / Hypothesis / Cause / Decision) so analyses become queryable graphs, not just documents.
- **v3.0 — Analysis Agent**: a multi-agent orchestration (Define Agent, Model Agent, Evidence Agent, Hypothesis Agent, Causality Agent, Prediction Agent, Optimization Agent, Report Agent) sharing one Analysis Graph.

See [`roadmap.md`](roadmap.md) for details.

## License

MIT — see [`LICENSE`](LICENSE).

## Author

Kevin ([@dvdface](https://github.com/dvdface)) · [SoloXLab](https://github.com/SoloXLab)
