# Best Practices

- **Don't let Model become a data dump.** A system model is a small number of well-chosen abstractions (10-20 objects, not 200). If everything feels essential, the scope from Phase 1 was probably too broad.
- **Timebox Observe.** Endless data exploration without hypothesis generation is a trap. Once 2-3 credible hypotheses emerge, move to Explain and let hypothesis testing guide further targeted observation.
- **Say "Missing Evidence" out loud.** It's tempting to smooth over gaps with a plausible-sounding inference. Don't. Flag the gap; let the human decide whether to close it or accept the risk.
- **One graph per relationship type.** Don't cram dependency edges and causal edges into the same diagram — it becomes unreadable and conflates "what could affect X" with "what does affect X."
- **Re-run Predict against reality when possible.** A prediction that's never checked against what actually happened is a wasted opportunity to calibrate confidence for next time.
- **Keep domain packs thin.** A domain pack (`domains/*.md`) should add objects, metrics, and known failure modes — it should not reimplement the six-phase pipeline. If a domain pack starts looking like its own methodology, something has gone wrong.
