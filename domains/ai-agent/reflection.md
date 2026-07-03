# Domain pack: AI Agent — Reflection / Self-critique Loops

## Key objects
Primary generation step, critique/reviewer step, revision step, stopping criterion.

## Key metrics
Improvement per reflection iteration (does quality actually increase?), iterations to convergence, cost overhead vs. quality gain.

## Common failure modes / root causes
- Reflection loop never terminates (no clear stopping criterion, or criterion never satisfiable)
- Critique step uses the same blind spots as the generation step (correlated errors, not independent review)
- Revision step "fixes" a critique by superficially changing wording without addressing the underlying issue
- Diminishing/negative returns after 1-2 iterations, but the loop runs many more anyway (wasted cost)

## Diagnostic approach
Plot a quality metric (if available) against iteration count across sample runs — if it plateaus or degrades after N iterations, the stopping criterion should be tightened to N regardless of the theoretical iteration budget.
