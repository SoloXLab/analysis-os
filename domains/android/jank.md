# Domain pack: Android — Jank / Frame Drops

## Key objects
Choreographer, RenderThread, SurfaceFlinger, BufferQueue, VSync, FrameTimeline, GPU driver.

## Key metrics
Jank rate (% frames exceeding budget), frame time p50/p90/p99, "Frozen frames" vs "Janky frames" (per Android Vitals definitions), FrameTimeline `deadline`, `actualEndTime`.

## Known process (simplified per-frame pipeline)
```
VSync -> Choreographer#doFrame -> [Input -> Animation -> Traversal (measure/layout/draw)]
  -> RenderThread sync+draw -> GPU render -> SurfaceFlinger composite -> display
```

## Common failure modes / root causes
- Main-thread work exceeding budget inside `doFrame` (heavy layout, overdraw-heavy custom view `onDraw`, GC pause)
- RenderThread/GPU-bound frames (overdraw, expensive shaders, large bitmap uploads)
- Buffer queue starvation/stalling (app producing faster/slower than SurfaceFlinger consumes)
- Missed VSync due to thermal throttling or CPU governor scaling down under load
- Animation using the wrong thread / not leveraging RenderThread-only properties

## Diagnostic approach
Use FrameTimeline in Perfetto to classify each janky frame's bottleneck stage (App deadline missed vs SF deadline missed vs GPU-bound), then drill into the specific slice on the relevant thread (main/render/GPU) for that frame.
