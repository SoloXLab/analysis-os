# Domain pack: Android — ANR (Application Not Responding)

## Key objects
Main thread (UI thread), Binder threads, AMS, InputDispatcher, Handler/Looper/MessageQueue, WatchDog.

## Key metrics
ANR rate (per DAU or per session), ANR type distribution (Input dispatching timeout / Broadcast timeout / Service timeout / ContentProvider timeout), main-thread block duration.

## Common failure modes / root causes
- Synchronous Binder call to a slow/blocked remote process from the main thread
- Main-thread lock contention (`synchronized` block held by a background thread doing I/O)
- Main-thread I/O (disk read/write, SharedPreferences.commit(), SQLite on main thread)
- Message queue backlog — too many/too-heavy `Handler.post` on main thread ahead of the blocking one
- GC pause coinciding with an input event window (memory pressure -> long GC -> ANR)
- Deadlock between main thread and a thread it's implicitly waiting on

## Diagnostic approach
1. Get the ANR trace / tombstone — identify what the main thread was doing at time of ANR (`"main" prio=5 tid=1 ...` stack).
2. If main thread is blocked on a lock, find the thread holding that lock and what *it* was doing.
3. If main thread is in Binder transaction, identify the remote process/service and whether *it* was blocked (cascading ANR).
4. Correlate with system state at the time (memory pressure / GC logs / CPU throttling / thermal).

## Recommended tooling
ANR trace files (`/data/anr/traces.txt` or via Play Vitals / vendor crash reporting), Perfetto system trace bracketing the ANR window, `dumpsys activity` for AMS-side state.
