# Phase 3 — Observe

**Goal:** collect evidence. Never explain before observing — explanations built on assumed-but-unchecked data are the single most common failure mode in AI-assisted analysis.

## Techniques to consider

- **Exploratory data analysis (EDA):** trend, distribution, variance, outliers
- **Relationships:** correlation, lead-lag analysis, cross-correlation
- **Structure over time:** timeline reconstruction, event sequencing
- **Visualization:** always prefer a chart/diagram over a table of numbers when the point is a *shape* (trend, distribution, spike)
- **Dimensionality/pattern discovery:** feature importance, SHAP, clustering, PCA
- **Anomaly detection:** where does the system deviate from its own baseline?

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
