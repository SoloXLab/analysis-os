# Domain pack: Distributed Systems

## Key objects
Service instances, load balancer, queue/broker, cache layer, database (primary/replica), circuit breaker, service mesh/sidecar.

## Key metrics
p50/p95/p99 latency, error rate, throughput/QPS, saturation (CPU/connection pool/queue depth), replication lag.

## Common failure modes / root causes
- Cascading failure: one slow dependency exhausts caller thread/connection pools, which then makes the caller slow to *its* callers
- Thundering herd on cache expiry or service restart
- Retry storms amplifying an initial small failure into an outage
- Split-brain / stale-read issues from replication lag under a naive read strategy
- Capacity cliff: performance degrades gracefully until a threshold, then collapses non-linearly (queueing theory — see `perf-modeling` skill for USL/Little's Law-based modeling)

## Diagnostic approach
Build the service dependency graph first (Phase 2 Model is non-negotiable here — distributed failures are almost always about dependency structure). Trace a single failing request end-to-end across service boundaries to find where latency/errors are actually introduced vs. merely propagated.
