# Domain pack: Android — Perfetto Trace Analysis (cross-cutting tool reference)

Perfetto is the primary evidence-collection tool for most Android domain packs above. This file is referenced by startup/anr/jank/binder/memory rather than duplicating tooling advice in each.

## Core slices/tracks to know
- `Choreographer#doFrame` — per-frame main-thread work
- `traversal`, `measure`, `layout`, `draw` — view hierarchy cost breakdown
- `RenderThread` track — GPU command submission cost
- FrameTimeline track — expected vs actual deadline per frame, App vs SF attribution
- Binder tracepoints — transaction-level IPC latency
- `bindApplication`, `activityStart`, `activityResume` — startup slices

## Workflow
1. Collect trace scoped tightly to the time window of interest (avoid huge traces that are slow to query).
2. Use SQL queries (`trace_processor_shell` or Perfetto UI query mode) to aggregate rather than eyeballing — especially for jank rate / percentile calculations across many frames.
3. Cross-reference with `dumpsys` / logcat timestamps for events not captured natively in the trace (app-specific business logic markers via `Trace.beginSection`).

See the `perf-trace-analyzer` and `perf-trace-collector` skills for the full operational workflow beyond what belongs in this domain pack.
