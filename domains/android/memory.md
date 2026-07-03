# Domain pack: Android — Memory

## Key objects
ART heap (Java/Kotlin objects), native heap (malloc), GraphicBuffer/ashmem, LMKD (Low Memory Killer Daemon), zRAM.

## Key metrics
PSS/RSS, Java heap size vs max, native heap growth rate, GC pause frequency/duration, OOM kill rate, LMKD kill rate & oom_score_adj at kill time.

## Common failure modes / root causes
- Java-side leaks (static references to Activity/Context, unregistered listeners, Handler leaks)
- Native leaks (missing `free`/`delete`, JNI global ref leaks)
- Bitmap-related memory pressure (uncompressed/oversized bitmaps, missing recycle in legacy code paths)
- Excess GraphicBuffer usage (too many/too-large surfaces)
- App placed in a low `oom_score_adj` tier incorrectly, making it an LMKD target sooner than expected

## Diagnostic approach
See `native-memory-analysis` skill for native-specific workflow (heapprofd, HWASan/ASan). For Java-side, `dumpsys meminfo`, heap dumps + LeakCanary-style reference chain analysis, and GC log correlation with jank/ANR windows.
