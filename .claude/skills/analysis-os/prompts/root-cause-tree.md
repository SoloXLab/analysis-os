# Prompt: Root Cause Tree

Use a tree (or fishbone diagram) once there are 3+ candidate causes, to make ranking and relationships visible rather than buried in prose.

```
Problem: <the Phase 1 problem statement>
│
├── Hypothesis A (confidence: high)
│     ├── Supporting evidence: ...
│     └── Contradicting evidence: (none / ...)
│
├── Hypothesis B (confidence: medium)
│     ├── Supporting evidence: ...
│     └── Contradicting evidence: ...
│
└── Hypothesis C (confidence: low — Missing Evidence)
      └── Would need: <what data/experiment would confirm or reject this>
```

For a fishbone/Ishikawa layout, group candidate causes into families relevant to the domain (e.g. for Android: App code / Framework / Kernel / Hardware / Config; for business: People / Process / Market / Product / Pricing) with the problem as the "spine".

## Weight-encoding rule (when factors are quantified)

If `explain.md` Step 4.3 produced a `β` (or any comparable effect-size number) for a factor, the diagram must encode it visually — a diagram where every branch looks the same weight is decoration, not information:

- **Line/bone thickness** ∝ `|β|` (or the qualitative equivalent: high/medium/low confidence mapped to thick/medium/thin) — the biggest lever should be visually obvious at a glance, not something the reader has to read a table to find.
- **Color by role** (from `explain.md` Step 4.4): essential = one color, mediating = a second, confounding = a muted/greyed color (visually de-emphasized — it shouldn't compete for attention with real causes), conditional/moderating = a third, distinct color.
- Each leaf/branch label should carry its numbers inline (`factor name  β=x.xx  r=x.xx  compression=x%`) rather than requiring a lookup in a separate table.
- If nothing was quantified (Tier D reasoning only), skip the numeric labels but keep the color-by-role convention — role classification doesn't require statistics, only the 5Why/mechanism reasoning from `explain.md`.
