# Visual Threat Detection — Adversarial Robustness on CCTV Systems

> Hybrid anomaly detection pipeline with adversarial attack and defense evaluation.  
> Built to explore the gap between ML benchmark performance and real-world CCTV security.

---

## What This Project Does

A two-component system that detects visual threats in CCTV footage — then deliberately tries to break it:

**Component 1 — Deployed Pipeline (Two-Stage)**  
YOLOv8 person detection → ByteTrack tracking → Rule-based anomaly head  
Detects: loitering, intrusion, unusual motion

**Component 2 — Learned Anomaly Model**  
Future-frame prediction (U-Net) trained on normal footage only  
Anomaly score = prediction error at test time  
Evaluated on UCSD Ped2 (frame-level AUC)

**Security Layer**  
Both components are attacked and defended:
- Physical: adversarial patches (Thys et al.) on YOLO
- Digital: FGSM / PGD on the VAD model
- Defenses: input transformations, adversarial training — benchmarked for latency vs. robustness

---

## Architecture

```
Camera Feed
    │
    ├── [Stage 1] YOLOv8 → ByteTrack → Rules Engine → Alert
    │                                                    ↑
    │                                             Loitering / Intrusion
    │
    └── [Stage 2] Frame Buffer → U-Net Predictor → Anomaly Score
```

---

## Datasets

| Dataset | Used For |
|---|---|
| UCSD Ped2 | VAD model training + evaluation |
| CUHK Avenue | (planned) cross-dataset generalization |

---

## Results

*Training in progress — numbers will be updated here*

| Component | Metric | Score |
|---|---|---|
| VAD Model | Frame-AUC (Ped2) | — |
| YOLO baseline | Patch attack success rate | — |
| Defense: JPEG (q=75) | Accuracy recovery | — |
| Defense: Adv. training | Accuracy recovery | — |

---

## Project Structure

```
visual-threat-detection/
├── pipeline/        # YOLO + ByteTrack + rules
├── vad/             # Future-frame prediction model
├── attacks/         # FGSM, PGD, adversarial patch
├── defenses/        # Input transforms, adv. training
├── demo/            # Streamlit UI + FastAPI backend
├── notebooks/       # Training and eval on Kaggle
├── THREAT_MODEL.md  # Full threat model doc
└── README_SECURITY.md
```

---

## Threat Model (Summary)

Full doc → [`THREAT_MODEL.md`](doc/THREAT_MODEL.md)

Realistic attack on a deployed CCTV system is **physical**, not digital:  
an adversarial patch printed on clothing breaks YOLO detection silently.  
Digital FGSM/PGD is used as a **lower-bound robustness probe** on the VAD model.

---

## Setup

```bash
conda create -n vtd python=3.10 -y
conda activate vtd
git clone https://github.com/ties2/visual-threat-detection
cd visual-threat-detection
pip install -r requirements.txt
```

Demo:
```bash
streamlit run demo/app.py
```

---

## Author

**Nirvana EL** — Cyber Intelligence Analyst | 9 years in cybersecurity  
[GitHub](https://github.com/ties2)

---

*Results and trained weights will be added as training completes on Kaggle.*