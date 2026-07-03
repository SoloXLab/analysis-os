# Methodology

## The pipeline

```
Define -> Model -> Observe -> Explain -> Predict -> Optimize
```

This ordering is deliberate and not arbitrary:

1. **Define** prevents analyzing the wrong problem.
2. **Model** prevents analyzing data without structural context (the #1 cause of spurious correlation-chasing).
3. **Observe** prevents explaining before evidence exists.
4. **Explain** prevents confusing correlation with causation.
5. **Predict** prevents recommending actions without understanding forward consequences.
6. **Optimize** prevents recommending actions that aren't traceable to a validated cause.

Each phase's output is a required input to the next. Skipping a phase should be a conscious, stated decision ("skipping Predict since this is a post-mortem, not a forecast"), not a silent omission.

## Fact / Inference / Hypothesis / Unknown

Every substantive claim in an Analysis OS report carries (implicitly or explicitly) one of these tags:

- **Fact** — directly observed/measured, verifiable
- **Inference** — a logical conclusion from facts, but not itself directly observed
- **Hypothesis** — a candidate explanation not yet confirmed or rejected
- **Unknown** — genuinely unresolved with current evidence

## Causal methods, ranked by strength of evidence they require

Weakest to strongest: correlation → lead-lag/Granger → controlled comparison / counterfactual → mechanism-backed causal inference (with a validated DAG or experiment). Analysis OS never presents a weaker-tier finding using stronger-tier language (e.g. never say "X causes Y" when only correlation was established).
