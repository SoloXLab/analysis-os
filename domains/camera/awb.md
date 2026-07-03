# Domain pack: Camera — Auto White Balance (AWB)

## Key objects
AWB statistics engine, color-temperature estimation model, gray-world / illuminant-detection algorithms.

## Key metrics
Color accuracy (Delta-E vs reference under standard illuminants), convergence time, stability under mixed lighting.

## Common failure modes
- Illuminant misclassification (e.g. tungsten mistaken for shade) causing visible color cast
- Instability/flicker in mixed-illuminant scenes (control loop oscillating between two color-temp estimates)
- Skin-tone or sky-color bias from gray-world assumption violation (large uniform colored surfaces)

## Diagnostic approach
Test against a standard illuminant set (D65, tungsten, fluorescent, mixed) with a reference color chart; compare AWB engine's estimated color temperature to ground truth per illuminant to isolate misclassification vs. convergence-speed issues.
