# Domain pack: Camera — ISP Pipeline Overview

## Key objects
Sensor, ISP (Image Signal Processor) pipeline stages (black-level correction, demosaic, denoise, sharpening, tone mapping), HAL3 camera stack, 3A engine (AE/AF/AWB), CamX/QCamera or vendor-equivalent.

## Key metrics
Frame latency (capture to output), 3A convergence time, preview FPS stability, still-capture shutter lag, HDR merge time.

## Known pipeline (simplified)
```
Sensor raw capture -> ISP front-end (BLC, lens shading, demosaic)
  -> 3A statistics collection -> ISP back-end (denoise, sharpen, tone map, color)
  -> HAL3 result -> App surface
```

## Common failure modes / root causes
- 3A statistics latency causing AE/AF/AWB convergence lag (often a sensor-to-ISP timing issue, not app-side)
- ISP back-end overload under high-resolution/high-FPS combined modes causing frame drops
- Tuning-parameter regressions after ISP firmware/tuning updates (color shift, noise increase)
- HAL3 pipeline stalls from result-callback backpressure on the app side

## Diagnostic approach
Correlate app-observed latency/FPS with vendor ISP debug logs and sensor timing metadata; isolate whether the bottleneck is sensor readout, ISP processing, or HAL/app-side consumption via per-stage timestamps if available.
