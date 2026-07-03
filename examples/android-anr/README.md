# Example: Android ANR Spike After Release

**Problem:** ContentProvider timeout ANRs increased 5x in the 48 hours after releasing version 3.4.0.

**System Model highlights:** ContentProvider `query()` invoked from a remote process via Binder; ANR fires if the provider doesn't respond within the platform timeout.

**Observation:** ANR traces show the main thread blocked inside a newly-added ContentProvider method, itself blocked on a `synchronized` lock also held by a background sync thread that's doing a large SQLite migration on first run after update.

**Hypothesis (confirmed):** The 3.4.0 release introduced a one-time DB schema migration that runs on a background thread but holds a lock also required by the ContentProvider's read path — any external query during the migration window blocks until migration completes, exceeding the ANR timeout for large datasets.

**Root cause:** Lock granularity too coarse — migration and read paths share a single lock instead of being isolated, and the migration was not benchmarked against the ANR timeout budget for large-DB users.

**Prediction:** Self-limiting — only affects the first run after update per device, so the spike will taper over ~1-2 weeks as the install base migrates. But large-DB users (power users, often high-value) are disproportionately affected.

**Optimization:** P0 — make migration non-blocking for the read path (either finer-grained locking or a "migration in progress" fast-fail response instead of blocking). P1 — add a pre-release benchmark gate for migration duration on large synthetic datasets.

**Unknowns:** Exact distribution of DB sizes in the install base wasn't available at analysis time — would sharpen the prediction of how long the tail lasts.
