# Compliance Gate (mandatory before delivering any Analysis OS output)

This file exists because of a real failure mode: every rule below already existed elsewhere in this skill (`model.md`, `explain.md`, `observe.md`, `report.md`) and got silently skipped anyway — because "the rule exists somewhere in the skill" and "the rule was actually applied this turn" are different things, and nothing forced a check between them. This is that check.

**A report that hasn't passed this gate is a draft, not a deliverable.**

## When to run this

Run the full gate for anything non-trivial — multi-factor analysis, root cause investigation, anything invoking a domain pack or `prompts/quantify-factors.md`. Run **Quick mode** (below) for short/informal requests where a full gate would be disproportionate.

## The gate

Go through this list literally, item by item, after drafting the report and before sending it. Each item's state must be one of:

- **Done** — actually executed on this specific analysis, this turn — not paraphrased, not promised, not "this is generally what the method finds."
- **Explicitly degraded** — attempted, hit a real constraint (no data, sample too small, no comparable cases), and the degradation is stated in the output, not hidden.
- **N/A** — genuinely doesn't apply here, with a one-line reason.

An item marked "Done" on the strength of describing what the technique usually shows, rather than having actually run it this turn, fails the gate — that is exactly the failure this file exists to catch.

```
[ ] Comparative discovery: horizontal and/or vertical comparison was actually
    run against real data/cases (search performed, real numbers pulled),
    not asserted from general knowledge alone.

[ ] 5Why: every retained hypothesis was drilled down until a real stop
    condition was hit (irreducible mechanism/policy/constant, or a named
    reason for stopping early) — no factor sits at its first-stated,
    surface-level form in the final report.

[ ] Quantification tier: for each retained factor, the tier (A/B/C/D)
    actually used is stated NEXT TO the factor in the output — not just
    described once in prose up top. If Tier A was attempted and downgraded
    (e.g. n too small, data unavailable), the attempt itself and the reason
    for downgrading are shown, not just the final tier label.

[ ] Factor role: every factor in the final list is tagged essential /
    mediating / confounding / moderating — not left as a flat, unranked list.

[ ] Robustness check: cross-group/cross-time stability was actually checked
    for the headline factor(s). If skipped, say so explicitly and say why.

[ ] Convergence: the response states why the analysis stopped where it did —
    either a threshold was met, or it's explicitly flagged "not converged,
    here's specifically what's still missing."

[ ] Visualization: if a diagram was implied or would materially help, it was
    actually rendered via a tool call THIS turn — never described in words
    as something that "would" be shown, and never left as a stated intention
    that doesn't appear in the output.

[ ] Plain-language annotation: first use of each technical/statistical term
    carries a plain-language parenthetical.

[ ] Data quality gate: missing-value / granularity / outlier / sample-size
    limitations were actually stated for any dataset used, however briefly —
    including exactly how much of the intended sample was actually covered
    (e.g. "13 of 31 provinces" is a materially different claim from
    "provincial data").

[ ] Every skipped or degraded item above is named out loud in the delivered
    response — not silently absent from it.
```

## Quick mode (short/informal requests)

State only the items that are non-trivial for this specific request, one line each: which tier was actually used, whether a diagram was rendered, and any hard degradations. Skip items that clearly don't apply (no domain pack invoked, no visualization warranted) without listing them.

## Self-test

Before finalizing, ask: *if the person who asked this question read only my compliance section, would they know exactly which parts of this analysis are solid and which parts I couldn't fully deliver on — or would they have to take my word for it?* If it's the latter, the gate hasn't actually been applied, only narrated.

## Relationship to other skills in Kevin's toolkit

This mirrors the self-critique loop pattern already used in `fault-tagger` / `module-tagger` — a mandatory final verification pass with an explicit pass/fail per rule, not an optional nicety bolted on at the end.
