# Prompt: System Model

Use this structure when writing out a Phase 2 System Model.

```
### Objects
- <entity 1>: <one-line role>
- <entity 2>: ...

### Structure
<architecture / hierarchy / topology description, or a diagram>

### Process (lifecycle)
Step1 -> Step2 -> Step3 -> ...

### Dependencies
See dependency-graph.md

### States
<state 1> -> <state 2> -> ... (with transition triggers)

### Resources consumed
<resource>: <how it's consumed>

### Constraints
<hard limit>: <value + consequence of violation>

### Invariants
- <thing that must always be true>

### Feedback loops
- <loop type> : <A -> B -> ... -> A, amplifying/dampening>
```

Keep it concrete — every entry should reference something real in the system being analyzed, not a generic placeholder.
