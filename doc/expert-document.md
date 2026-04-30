# this document provide for expert people to know more about project



visual-threat-detection/
├── README.md                  ← ML-flavored (fill numbers later)
├── README_SECURITY.md         ← Security-flavored version
├── THREAT_MODEL.md            ← The differentiating doc — we build this now
├── requirements.txt
├── Dockerfile
├── .github/
│   └── workflows/ci.yml
├── data/
│   └── download_ucsd.sh       ← Script to pull UCSD Ped2
├── pipeline/
│   ├── __init__.py
│   ├── detector.py            ← YOLO + ByteTrack stage
│   └── rules.py               ← Loitering/intrusion logic
├── vad/
│   ├── __init__.py
│   ├── model.py               ← Future-frame prediction (U-Net)
│   ├── train.py
│   └── evaluate.py            ← Frame-AUC computation
├── attacks/
│   ├── fgsm_pgd.py            ← Digital attacks on VAD model
│   └── adv_patch.py           ← Physical patch attack on YOLO
├── defenses/
│   ├── input_transforms.py    ← JPEG compression, bit-depth reduction
│   └── adv_training.py
├── demo/
│   ├── app.py                 ← Streamlit UI
│   └── api.py                 ← FastAPI backend
└── notebooks/
├── 01_data_exploration.ipynb
├── 02_vad_training.ipynb
└── 03_attack_eval.ipynb

# notebooks

notebooks/02_vad_training.ipynb      ← This is  main one (train the U-Net)
notebooks/01_data_exploration.ipynb  ← Run this first (check the dataset)
notebooks/03_attack_eval.ipynb       ← Run this after training (FGSM/PGD)