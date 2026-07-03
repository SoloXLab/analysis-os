# Domain pack: AI Agent — Agentic Loops (ReAct-style)

## Key objects
Think/Act/Observe cycle, action space, environment/tool feedback, loop-termination condition.

## Key metrics
Loop iterations to task completion, wasted/redundant actions, loop-abandonment rate (giving up without completing).

## Common failure modes / root causes
- Agent repeats the same failed action without adapting (no effective use of the Observe feedback)
- Action space too large/ambiguous, causing indecisive/thrashing behavior between similar actions
- Environment feedback is noisy or delayed, causing the agent to act on stale state
- No fallback/escalation strategy when stuck, leading to silent infinite loop or premature abandonment

## Diagnostic approach
Trace the Think/Act/Observe sequence for a stuck run; check specifically whether each "Think" step actually incorporates the most recent "Observe" result, or whether it's re-deriving from an earlier, now-stale belief state (a common root cause of repeated failed actions).
