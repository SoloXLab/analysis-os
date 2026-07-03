# Roadmap

## v1.0 — Analysis Framework (current)
- [x] Universal Define → Model → Observe → Explain → Predict → Optimize loop
- [x] Claude Code skill packaging (`.claude/skills/analysis-os/`)
- [x] Domain packs: Android, Camera/ISP, AI Agent (deep); Distributed/UX/Business/Finance (index-level)
- [x] Report templates
- [x] Worked examples
- [ ] Port skill format to OpenCode / Cursor Rules / Codex conventions (currently Claude Code-native only)
- [ ] LangGraph reference implementation of the pipeline as an actual executable graph (not just a prompt structure)

## v2.0 — Analysis Graph
- [ ] Define the Analysis Graph schema formally (see `docs/graph-model.md` for the current node/edge type preview)
- [ ] Persist analyses as graphs (e.g. in a local SQLite/graph store) instead of only Markdown reports
- [ ] Cross-analysis querying ("show all past root causes tagged Binder contention")
- [ ] Diffing: compare two analyses of the same system over time

## v3.0 — Analysis Agent
- [ ] Multi-agent orchestration: Define / Model / Evidence (+ Trace/Log sub-agents) / Hypothesis / Causality / Prediction / Optimization / Report agents, per `docs/architecture.md`
- [ ] Shared Analysis Graph as the common state across all agents
- [ ] Parallel evidence-gathering sub-agents with defined merge semantics

## Non-goals (for now)
- A hosted/SaaS product — this stays a portable, model-agnostic framework
- Replacing domain-specific tooling (Perfetto, akshare, etc.) — Analysis OS orchestrates reasoning around evidence, it doesn't collect evidence itself

Contributions toward any unchecked item welcome — see `CONTRIBUTING.md`.
