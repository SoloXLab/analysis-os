# Domain pack: Camera — Auto Focus (AF)

## Key objects
AF statistics engine (contrast-detect and/or PDAF), lens actuator, focus search algorithm.

## Key metrics
AF convergence time, focus accuracy (hit rate), hunting frequency, low-light AF success rate.

## Common failure modes
- PDAF confidence low in low-contrast or low-light scenes, falling back to slower contrast-detect search
- Actuator response lag/hysteresis vs. algorithm's assumed lens response model
- Focus search overshoot/undershoot causing visible hunting
- Macro/close-focus edge cases outside the calibrated lens position range

## Diagnostic approach
Compare AF statistics confidence values against actual focus outcome across a controlled scene set; separate algorithm-side issues (search strategy) from actuator-side issues (mechanical response) using lens-position telemetry.
