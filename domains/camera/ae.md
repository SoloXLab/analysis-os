# Domain pack: Camera — Auto Exposure (AE)

## Key objects
AE statistics engine, exposure/gain control loop, metering regions, flicker detection.

## Key metrics
AE convergence time, exposure stability (flicker/oscillation), over/under-exposure rate in varied lighting.

## Common failure modes
- Slow convergence in low light (statistics too sparse, control loop gain too conservative)
- Oscillation ("hunting") from control loop gain too aggressive
- Incorrect metering region weighting causing subject under/over-exposure
- Flicker-detection misfiring under mixed lighting (LED + sunlight)

## Diagnostic approach
Treat as a control-loop system (see `perf-modeling` skill for control-loop/feedback-loop modeling): plot exposure/gain over time against target, characterize as under-damped (oscillation) or over-damped (slow convergence), tune accordingly.
