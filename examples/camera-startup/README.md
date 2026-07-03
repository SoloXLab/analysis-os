# Example: Camera App Launch-to-Preview Latency Regression

**Problem:** Time from tapping the camera icon to a stable preview frame increased from ~350ms to ~600ms on a specific chipset after a camera HAL update.

**System Model highlights:** App launch -> HAL3 camera session open -> sensor stream start -> 3A convergence -> stable preview. Key constraint: perceived "instant camera" UX threshold is generally cited around 400-500ms.

**Observation:** Vendor ISP debug logs show HAL session-open time itself unchanged, but 3A (specifically AE) convergence time roughly doubled after the HAL update in typical indoor lighting.

**Hypothesis (confirmed):** The HAL update changed default AE control-loop gain to a more conservative value (likely to reduce exposure oscillation reported in a prior tuning pass), trading convergence speed for stability.

**Root cause:** A tuning trade-off made for a different bug (exposure oscillation) had an unintended regression on convergence latency — the two goals (fast convergence, stable/non-oscillating exposure) were not jointly optimized.

**Prediction:** Stable at the new (worse) latency until the tuning is revisited; not self-correcting.

**Optimization:** P1 — retune AE control loop gain schedule to recover convergence speed in well-lit indoor conditions specifically (where oscillation risk is lower) while retaining the conservative gain for low-light where oscillation was originally observed — i.e. make gain scene-adaptive rather than a single global value.

**Unknowns:** Whether the original oscillation bug reproduces under the faster gain in low light specifically — needs targeted re-testing before shipping the fix.
