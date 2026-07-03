# Domain pack: Camera — HDR

## Key objects
Multi-frame capture controller, exposure bracketing logic, ghost/motion detection, tone-mapping/merge engine.

## Key metrics
HDR merge latency, ghosting artifact rate (motion scenes), dynamic range gain (stops), shutter lag in HDR mode.

## Common failure modes
- Ghosting from misaligned/misregistered frames in motion scenes (alignment algorithm failing on fast subject motion)
- Merge latency exceeding user-perceptible shutter-lag budget under high-resolution capture
- Tone-mapping producing unnatural results (over-processed "HDR look") — a tuning/perceptual issue, not strictly a defect, but worth separating from true technical failures
- Bracket exposure selection mismatched to actual scene dynamic range (clipped highlights or crushed shadows despite HDR mode)

## Diagnostic approach
Separate "objective" failures (ghosting, latency, clipping) from "subjective/tuning" issues (perceived over-processing) since they require different resolution paths — the former is a bug, the latter is a tuning/product decision.
