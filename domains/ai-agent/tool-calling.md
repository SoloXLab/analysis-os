# Domain pack: AI Agent — Tool Calling

## Key objects
Tool schema/registry, tool-call request (name + args), tool result, error-handling/retry layer.

## Key metrics
Tool-call success rate, malformed-argument rate, retry count, tool-selection accuracy (right tool for the task).

## Common failure modes / root causes
- Argument hallucination (model invents a parameter value not grounded in available context)
- Wrong tool selected when multiple tools have overlapping descriptions (schema/description ambiguity)
- Tool result not correctly parsed/consumed by the model on the next turn (format mismatch)
- Missing error handling causing a failed tool call to be silently treated as success

## Diagnostic approach
For each failure, classify as: (1) tool-selection error, (2) argument-construction error, (3) result-consumption error. This maps directly to whether the fix belongs in tool descriptions, prompt/schema design, or result-formatting.
