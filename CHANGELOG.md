# Changelog

## [1.0.0] - 2026-07-03
### Added
- Initial Analysis OS v1.0 framework: Define → Model → Observe → Explain → Predict → Optimize pipeline as a Claude Code skill (`.claude/skills/analysis-os/`)
- Core docs: philosophy, methodology, architecture, graph-model preview, analysis loop, best practices
- Domain packs: Android (startup, ANR, jank, binder, memory, perfetto), Camera/ISP (isp, AE, AF, AWB, HDR), AI Agent (workflow, planner, tool-calling, reflection, loop), plus index packs for distributed systems, UX, business, and finance
- Templates: analysis-report, system-model, hypothesis, root-cause, decision, postmortem
- Worked examples across Android startup/ANR, camera startup, AI agent loop, vehicle sales, and distributed system incident
- Roadmap for v2.0 (Analysis Graph) and v3.0 (multi-agent orchestration)

## [1.1.0] - 2026-07-03
### Added
- Comparative discovery (horizontal/vertical comparison) integrated into `model.md`, with new `prompts/comparison-analysis.md` template — actively hunts for factors the initial system model missed instead of relying only on brainstorming
- Mandatory recursive 5Why drill-down on every hypothesis in `explain.md` (Step 4.2) — factors can no longer be accepted at a surface-level label
- Tiered quantification method (`explain.md` Step 4.3 + new `prompts/quantify-factors.md`): standardized β, single-variable r, compression rate, VIF, with graceful degradation to mechanism-based reasoning (explicitly labeled as such) when data isn't available
- Factor role classification — Essential / Mediating / Confounding / Moderating (`explain.md` Step 4.4) — replacing simple root-cause ranking, to prevent reporting a mediating factor as if it were the root cause
- Robustness / cross-group validation (`explain.md` Step 4.5) — flags factors whose effect isn't stable across sub-groups/time periods as "conditional"
- Explicit convergence criteria for when to stop iterating Model/Explain (`explain.md` Step 4.7)
- Data-quality gate in `observe.md` (missing-value threshold, granularity alignment, outlier handling) before evidence is trusted
- Mandatory plain-language annotation glossary and weight-encoded visualization rules in `report.md` / `prompts/root-cause-tree.md`
- Explicit user checkpoints (after Define, after Model, after final report) for long/high-stakes analyses

### Changed
- SKILL.md thinking rules updated to reference the above; version bumped to 1.1

These additions were absorbed from the `factor-analyzer` skill's quantitative rigor (5Why depth, r/β/compression statistics, mandatory visualization) while keeping Analysis OS general-purpose and usable without data (Tier D fallback).
