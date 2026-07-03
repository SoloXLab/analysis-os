# Example: LangGraph Agent Stuck in Retry Loop

**Problem:** A LangGraph-based bug-triage agent occasionally consumes 10x expected token budget on certain inputs without completing, requiring manual kill.

**System Model highlights:** Fan-out/fan-in graph: a Classifier node dispatches to N tagger sub-agents, then a Merge node combines results before returning. Termination is expected once all sub-agent branches report back to Merge.

**Observation:** Trace logs for a stuck run show one sub-agent (fault-tagger) repeatedly calling the same tool with slightly reworded arguments, never reaching a terminal state, while other branches completed normally and are waiting at Merge.

**Hypothesis (confirmed):** The stuck sub-agent's tool call returns a validation error for malformed XML-tag output; the agent's self-correction prompt re-attempts generation but the underlying cause (an ambiguous taxonomy category in the input bug description) isn't resolvable by rewording — it needs a fallback ("uncertain/needs human review") path that doesn't exist.

**Root cause:** Missing fallback/termination condition — the retry loop had no maximum-attempts cutoff and no "graceful uncertain" output option, so an unresolvable ambiguous case degrades to infinite retry instead of a bounded uncertain-classification result.

**Prediction:** Will recur on any future bug description that hits genuine taxonomy ambiguity — not a one-off, since the taxonomy itself has known edge cases.

**Optimization:** P0 — add a max-retry cap (e.g. 3 attempts) with fallback to an explicit "uncertain — needs human review" tag rather than infinite retry. P2 — review the taxonomy for the specific ambiguous category that triggered this and consider adding a category or disambiguation rule.

**Unknowns:** How frequently this specific ambiguity pattern occurs across historical inputs wasn't measured — would help prioritize the P2 taxonomy fix.
