# Domain pack: AI Agent — Workflow / Orchestration

## Key objects
Orchestrator, sub-agents/nodes, shared state/context, tool registry, message history, checkpoint/memory store.

## Key metrics
Task success rate, step count to completion, token cost per task, latency per step, retry rate.

## Common failure modes / root causes
- Context window overflow causing silent truncation of critical earlier state
- Ambiguous handoff between orchestrator and sub-agent (sub-agent doesn't know what orchestrator already resolved)
- State desync between parallel sub-agents writing to shared context without a merge strategy
- Over-broad tool permissions causing an agent to take an unintended irreversible action
- Missing termination condition causing infinite loop between two agents (A asks B, B asks A back)

## Diagnostic approach
Reconstruct the full message/tool-call trace for a failed run; identify at which step the agent's belief state diverged from ground truth, and trace backward to the originating tool result or prompt segment that caused the divergence.
