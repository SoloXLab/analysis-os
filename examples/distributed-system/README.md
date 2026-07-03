# Example: Cascading Latency Incident

**Problem:** API gateway p99 latency spiked from 200ms to 8s for 12 minutes, affecting all downstream services.

**System Model highlights:** Gateway -> Auth service -> User service -> DB (primary). Gateway and Auth service share a connection pool sized for normal load.

**Observation:** Traces show Auth service latency spiking first (DB primary had a slow query from an unrelated batch job), then Gateway's connection pool to Auth exhausted as requests piled up waiting, causing Gateway itself to appear broadly slow/unavailable even for requests not touching Auth.

**Hypothesis (confirmed):** Classic cascading failure — a slow dependency (DB, due to the batch job) caused Auth service latency to spike, which exhausted Gateway's shared connection pool, which then made Gateway slow for *all* traffic, not just Auth-dependent traffic — the failure propagated and amplified beyond its origin.

**Root cause:** Two compounding structural issues: (1) an unthrottled batch job allowed to run a slow query against the primary DB during peak hours, (2) Gateway's connection pool to Auth was not isolated/bulkheaded from pools serving other downstream services, so Auth-specific slowness became gateway-wide slowness.

**Prediction:** Will recur whenever a similarly slow query hits the primary during peak load, regardless of the specific batch job — the structural vulnerability (shared pool, unthrottled batch access to primary) is the real risk, not this one incident.

**Optimization:** P0 — move batch jobs to a read replica, never primary. P0 — bulkhead Gateway's connection pools per downstream service so one slow dependency can't exhaust capacity needed for others. P1 — add DB query timeout + circuit breaker on Auth's DB calls specifically.

**Unknowns:** Whether other batch jobs have similar unthrottled primary-DB access — recommend an audit beyond just the one implicated in this incident.
