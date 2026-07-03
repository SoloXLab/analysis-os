# Domain pack: AI Agent — Planner

## Key objects
Planner (task decomposition step), plan representation (list/tree/graph of subtasks), replanning trigger, executor.

## Key metrics
Plan quality (steps needed vs. optimal), replanning frequency, plan-execution divergence rate.

## Common failure modes / root causes
- Planner decomposes at the wrong granularity (too coarse to be actionable, or too fine causing excessive overhead)
- No replanning trigger when an executed step's result invalidates the rest of the plan (plan drift)
- Planner hallucinates a subtask that has no corresponding available tool/capability
- Circular dependency between planned subtasks (subtask B implicitly requires output of subtask C which requires B)

## Diagnostic approach
Compare the planned task graph against the actually-executed sequence; flag every point of divergence and classify each as (a) expected adaptive replanning or (b) a planning defect that should have been caught before execution.
