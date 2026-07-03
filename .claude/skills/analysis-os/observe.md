# Phase 3 — Observe

**Goal:** collect evidence. Never explain before observing — explanations built on assumed-but-unchecked data are the single most common failure mode in AI-assisted analysis.

## Techniques to consider

- **Exploratory data analysis (EDA):** trend, distribution, variance, outliers
- **Relationships:** correlation, lead-lag analysis, cross-correlation
- **Structure over time:** timeline reconstruction, event sequencing
- **Visualization:** always prefer a chart/diagram over a table of numbers when the point is a *shape* (trend, distribution, spike)
- **Dimensionality/pattern discovery:** feature importance, SHAP, clustering, PCA
- **Anomaly detection:** where does the system deviate from its own baseline?

## Data quality gate (check before trusting any dataset)

Run this check before a dataset feeds into Explain — silently analyzing low-quality data is a common source of confidently wrong conclusions:

- **Missing values**: if a candidate factor's data is missing for more than ~30% of the observations, downweight or exclude it rather than imputing silently.
- **Granularity mismatch**: if factors come from sources with different time granularity (e.g. daily metric vs. quarterly factor), resample/align before comparing — never eyeball two series with different sampling rates as if they line up.
- **Outliers**: flag them explicitly rather than silently dropping or silently including them; report the conclusion with and without them if they materially change the result (see Step 4.5 robustness check in `explain.md`).

## Discipline

- If a needed data source doesn't exist or wasn't provided, say **"Missing Evidence"** — do not backfill with a plausible-sounding number.
- Distinguish a single anecdote from a statistically supported pattern. One crash log is an observation; "this happens 40% of the time" requires a denominator.
- Record both what supports and what *contradicts* the leading hypothesis so far — selectively citing only confirming evidence is a bias to actively guard against.

## Deliverable: Evidence Report

A structured list of observations, each tagged with:
```
Observation:  <what was seen>
Source:       <trace / log / metric / user report / dataset>
Confidence:   <high / medium / low>
Supports:     <which hypothesis this bears on, if known yet>
```
