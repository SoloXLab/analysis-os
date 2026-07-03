# Domain pack: Android — Binder / IPC

## Key objects
Binder driver (kernel), Binder thread pool (per process, typically 15 max), transaction buffer, oneway vs two-way calls, ServiceManager.

## Key metrics
Binder transaction latency, Binder thread pool exhaustion events, transaction buffer usage (1MB per process default), oneway queue depth.

## Common failure modes / root causes
- Synchronous (two-way) Binder call from main thread to a slow remote service
- Binder thread pool exhaustion in a high-fanout service (too many concurrent transactions)
- Transaction buffer overflow (`TransactionTooLargeException`) from oversized Parcelable payloads
- oneway call flooding causing queue backlog and out-of-order delivery surprises
- Priority inversion: low-priority process holding a Binder thread that a high-priority caller is blocked on

## Diagnostic approach
`dumpsys binder_calls_stats` or Perfetto Binder tracepoints for transaction-level latency; identify caller/callee pair and whether the call was oneway or blocking; check remote process's thread pool saturation via `/proc/<pid>/status` or `dumpsys`.
