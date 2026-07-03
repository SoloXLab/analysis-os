# Report Assembly

After all six phases are complete (or as many as the request called for), assemble the final deliverable using `../../../templates/analysis-report.md` as the skeleton.

## Rules

- Every claim in the report must be traceable to a phase artifact — do not introduce new facts at report time that weren't established in Observe/Explain.
- Keep the **Unknowns** section honest. A report with no unknowns on a non-trivial system is a red flag that evidence was overstated somewhere upstream.
- If the user asked a narrow question ("just tell me the likely cause"), it's fine to lead with a short direct answer and fold the full phase breakdown into supporting detail below it — but the phase discipline (Fact vs Hypothesis, model before explain) still has to have happened, even if compressed in the final text.
- Prefer at least one diagram (system model, dependency graph, timeline, or root-cause tree) in any report covering a non-trivial system — see `prompts/`.

## Output skeleton

```
## 1. Problem
## 2. System Model
## 3. Observations
## 4. Hypotheses
## 5. Root Cause
## 6. Prediction
## 7. Optimization
## 8. Unknowns
```
