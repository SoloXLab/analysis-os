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
