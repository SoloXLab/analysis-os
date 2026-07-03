# Example: Android Cold Start Regression

**Problem:** TTID p90 regressed from 800ms to 1400ms on Pixel 9 / Android 15 over the last 2 weeks, no OS update in that window.

**System Model highlights:** Zygote fork -> Application.attach -> ContentProvider init -> Application.onCreate -> Activity lifecycle -> first draw -> TTID. Key invariant: no synchronous network calls should occur before first draw.

**Observation:** Perfetto trace comparison (last-known-good vs regressed build) shows a new 400ms slice inside `Application.onCreate`, attributable to a newly-added SDK's synchronous initialization call.

**Hypothesis (confirmed):** A newly integrated analytics SDK performs synchronous disk I/O (reading a config file) during `Application.onCreate`, blocking the main thread before any UI work can proceed.

**Root cause:** SDK initialization contract mismatch — the SDK was integrated using its synchronous init API instead of the async variant available in the same SDK version.

**Prediction:** If unaddressed, TTID will remain regressed for all users on this build; no auto-recovery expected since it's a code-path issue, not transient load.

**Optimization:** P0 — switch to the SDK's async init API, defer non-critical init to after first frame (e.g. via `Application.registerActivityLifecycleCallbacks` post-first-draw hook). Expected impact: full recovery to ~800ms baseline. Low risk (SDK's own supported API), low cost (single call-site change).

**Unknowns:** Whether other recently-added SDKs have similar synchronous-init anti-patterns not yet surfaced in this specific trace comparison — recommend an audit pass across all `Application.onCreate` SDK inits.
