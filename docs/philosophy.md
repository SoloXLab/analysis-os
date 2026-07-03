# Philosophy

## Everything is a system

Every system — software, hardware, an organization, a market, a body — can be described through the same five lenses:

- **Structure** — how its parts are organized
- **Behavior** — how it acts and reacts
- **State** — what condition it's currently in
- **Constraints** — what limits it
- **Evolution** — how it changes over time

Analysis OS treats these as universal, domain-independent categories. Swap "AMS/Activity/Binder" for "Customer/Channel/SKU" and the same modeling discipline applies.

## Understanding beats data-mining

It is easy — and tempting for an LLM — to jump from a pile of data straight to a plausible-sounding narrative. Analysis OS rejects that shortcut. A model of the system must exist *before* data is interpreted, because the model is what tells you which correlations are meaningful and which are noise.

## Explicit uncertainty is a feature, not a weakness

A report that never says "Unknown" or "Missing Evidence" is not more confident — it's less honest. Analysis OS requires every claim to be tagged Fact / Inference / Hypothesis / Unknown, so the reader can calibrate trust claim-by-claim instead of trusting (or distrusting) the whole document uniformly.

## The framework is the product, not the prompt

A single giant prompt is brittle and hard to extend. Analysis OS is built as composable phases (Define/Model/Observe/Explain/Predict/Optimize) and swappable domain packs, so new fields can be added without touching the reasoning core, and the reasoning core can be improved without breaking existing domain packs.
