# Project Scope

## Problem

Modern CCTV-based security systems rely heavily on computer vision models to detect threats automatically — yet the adversarial robustness of these systems is rarely evaluated before deployment. A model that achieves high accuracy on a benchmark dataset can fail silently when faced with a deliberately crafted input: a printed patch on a jacket, a subtle pixel-level perturbation injected into the video feed, or an unusual motion pattern the model has never seen.

The gap between benchmark performance and real-world robustness is the problem this project addresses. Specifically: **how much does a hybrid visual threat detection system degrade under adversarial attack, and what is the cost of defending against it?**

---

## Scenario

A mid-size facility (office building, transit hub, or campus) operates a CCTV network monitored by an AI-assisted system. The system is expected to flag anomalous events — loitering, unauthorized zone entry, unusual crowd behavior — in real time without continuous human attention.

Two adversaries are considered:

**Adversary 1 — Physical attacker.** A person wearing an adversarial patch designed to suppress YOLO person detection. The attacker moves through a monitored zone without triggering the loitering or intrusion rules, because the tracker never acquires a stable ID. No pixel-level access to the feed is required — the attack is carried out entirely in the physical world.

**Adversary 2 — Feed-level attacker.** An insider or compromised node with access to the video stream. The attacker applies imperceptible digital perturbations (FGSM / PGD) to incoming frames, causing the learned anomaly model to consistently underestimate the anomaly score and suppress alerts.

Both scenarios are evaluated in this project. The physical attack reflects the realistic threat to a deployed CCTV system. The digital attack serves as a lower-bound robustness probe: if the model fails under constrained digital perturbation, it will not survive physical-world attacks.

---

## Success Criteria

| Criterion | Target |
|---|---|
| VAD model trained and evaluated | Frame-level AUC ≥ 0.70 on UCSD Ped2 |
| Adversarial patch attack implemented | Detection suppression rate measured and reported |
| FGSM / PGD attack implemented | Anomaly score degradation measured at ε = 8/255 |
| At least two defenses benchmarked | Accuracy recovery and latency cost both reported |
| Working demo | Streamlit app runs on a video clip end-to-end |
| Threat model documented | `THREAT_MODEL.md` covers assets, adversaries, attack surface, mitigations |
| Reproducible | Any reviewer can clone the repo, follow README, and reproduce evaluation results |

The project is considered complete when all seven criteria are met and results are filled into the README results table. A blog post summarizing findings is a stretch goal.