# Domain pack: Android — Cold/Warm Start

## Key objects
Zygote, ActivityManagerService (AMS), ActivityThread, Application, Activity, WindowManagerService, SurfaceFlinger, PackageManagerService, ART/JIT, ContentProvider (early init), Choreographer.

## Key metrics
TTID (Time To Initial Display), TTFD (Time To Full Display), reportFullyDrawn timing, App Startup library init cost, class-loading/verification cost (ART), first-frame render latency.

## Known process (simplified)
```
Zygote fork -> Application.attach -> ContentProvider init -> Application.onCreate
  -> Activity.onCreate -> Activity.onStart -> Activity.onResume
  -> first traversal -> first draw -> SurfaceFlinger composite -> TTID
  -> (async: images/data load) -> reportFullyDrawn -> TTFD
```

## Common failure modes / root causes
- Heavy `Application.onCreate` (SDK inits, especially synchronous 3rd-party SDK init)
- ContentProvider chain doing disk/network I/O on the main thread
- Class verification cost from very large or poorly structured APKs (no baseline profile)
- Main-thread I/O in `Activity.onCreate`/`onStart`/`onResume`
- Layout inflation cost (deep view hierarchies, custom view measure/layout cost)
- Binder contention with AMS/WMS during high system load (cold start under memory pressure)
- Zygote fork cost itself elevated (system-wide, not just this app) — check system-wide launch metrics, not just this app's

## Recommended trace tooling
Perfetto (`Activity#onCreate`, `bindApplication`, `activityStart`, `traversal`, `Choreographer#doFrame` slices), Macrobenchmark `StartupTimingMetric`, `am start -W` for quick TTID/TTFD sanity check.
