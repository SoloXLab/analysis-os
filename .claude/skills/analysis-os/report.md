# Report Assembly

After all six phases are complete (or as many as the request called for), assemble the final deliverable using `../../../templates/analysis-report.md` as the skeleton.

## Rules

- Every claim in the report must be traceable to a phase artifact — do not introduce new facts at report time that weren't established in Observe/Explain.
- Keep the **Unknowns** section honest. A report with no unknowns on a non-trivial system is a red flag that evidence was overstated somewhere upstream.
- If the user asked a narrow question ("just tell me the likely cause"), it's fine to lead with a short direct answer and fold the full phase breakdown into supporting detail below it — but the phase discipline (Fact vs Hypothesis, model before explain) still has to have happened, even if compressed in the final text.
- Prefer at least one diagram (system model, dependency graph, timeline, or root-cause tree) in any report covering a non-trivial system — see `prompts/`. When factors were quantified, the diagram must use the weight-encoding rule in `prompts/root-cause-tree.md` (thickness/color mapped to real numbers, not decorative).

## Mandatory plain-language annotation

The first time any technical/statistical term appears in the report, attach a short parenthetical in plain language — this is what makes the report usable by someone without a stats or domain background, not just by another analyst. Keep each annotation under ~20 words, and don't explain one jargon term with another.

Reuse this glossary directly where applicable (extend it for domain-specific terms as needed):

| Term | Plain-language annotation |
|---|---|
| standardized β | independent influence of a factor after removing every other factor's effect |
| single-variable r | how strongly a factor moves with the outcome on its own — can be misleading |
| compression rate | how much of a factor's apparent effect is actually borrowed from another factor |
| mediating factor | not the root cause itself — the messenger for a deeper root cause |
| confounding variable | changes alongside the real cause, making you think it IS the cause |
| conditional factor | only matters in specific circumstances — swap the context and it stops mattering |
| VIF | how tangled two factors are with each other — too tangled and you can't credit either one individually |
| Granger causality | tests which variable's past predicts the other's future — not proof of true causation |
| p-value | probability the result is a fluke; conventionally <0.05 means probably not chance |
| R² | share of the outcome's variation the model explains, e.g. 0.7 = 70% explained |

## User checkpoints (for long/high-stakes analyses)

For anything beyond a quick informal request, confirm with the person at these points rather than running the entire pipeline unsupervised and risking a large wasted effort in the wrong direction:
1. **After Define** — confirm the problem statement/scope/metrics are right before building a System Model around them.
2. **After Model** (including comparative discovery) — confirm the factor candidate list before spending effort on Observe/Explain for the wrong set of factors.
3. **After the report is assembled** — confirm the conclusion lands correctly before treating it as final.

Short/simple requests can skip explicit checkpoints and just state assumptions inline as they're made.

## Compliance visibility (required, not just internal)

Running `checklist.md`'s gate internally and then writing a clean-looking report is not enough — if a requirement was degraded or skipped, the person reading the report needs to see that, not just trust that it was handled. For any non-trivial analysis, close the response with a short, honest account of what was actually done vs. degraded (tier used per factor, whether a diagram was actually rendered, sample coverage of any dataset, what didn't converge). This doesn't need `checklist.md`'s full internal checkbox format verbatim — it needs the same information stated in plain prose so the person can tell, without asking, which parts of the analysis are solid and which parts hit a real limit.

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
