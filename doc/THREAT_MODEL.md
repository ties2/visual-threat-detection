# Threat Model — Visual Threat Detection System

## System Description
Hybrid CCTV anomaly detection pipeline:
YOLOv8 (detection) → ByteTrack (tracking) → Rule engine (loitering/intrusion)
+ Future-frame prediction model (learned anomaly scoring)

## Assets
- Camera feed integrity
- Detection accuracy (no missed threats, no false alarms)
- System availability (real-time constraint: <100ms/frame)

## Adversaries
| Adversary | Goal | Capability |
|---|---|---|
| Physical attacker | Evade person detection | Can modify own appearance (clothing, patches) |
| Insider / feed attacker | Inject frames into feed | Pixel-level access to stream |
| DoS adversary | Saturate false positives | Can place objects in scene |

## Attack Surface
### Realistic (physical)
- Adversarial patch (Thys et al.) — printed pattern breaks YOLO person class
- Adversarial clothing — texture fooling detection at distance
- IR/lighting attack — overexpose camera sensor

### Contrived (digital, used as lower-bound probe)
- FGSM (ε=8/255) on future-frame prediction input
- PGD (ε=8/255, 40 steps) on future-frame prediction input
> If the model fails under digital attack, physical attacks are hopeless.

## Defenses Evaluated
- Input transformations: JPEG compression (q=75), bit-depth reduction (5-bit)
- Feature squeezing
- Adversarial training on backbone

## Out of Scope
- Model theft / extraction
- Network-layer attacks on the camera stream