🛡️ CyberSentry



Intrusion Detection System using RF, CatBoost, BiLSTM, and Attention mechanisms on the CICIDS2017 dataset.


![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange?style=for-the-badge&logo=tensorflow)
![CatBoost](https://img.shields.io/badge/CatBoost-Latest-yellow?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Dataset](https://img.shields.io/badge/Dataset-CICIDS2017-red?style=for-the-badge)

---

## 📌 Overview

**CyberSentry** is a hybrid, multi-class Network Intrusion Detection System (IDS) that combines the power of classical ensemble learning with deep learning to detect cyberattacks with high accuracy and explainability.

It uses a **stacked ensemble** approach:
- 🌲 **Random Forest** — captures non-linear feature relationships
- 🐱 **CatBoost** — gradient boosting for robust tabular learning
- 🧠 **BiLSTM + Attention** — deep learning meta-classifier on ensemble outputs
- 📊 **SHAP + LIME** — full explainability pipeline
- 🎯 **Calibration** — probability calibration for reliable confidence scores

---

## 🏗️ Architecture

```
Raw Network Traffic (CICIDS2017)
          │
          ▼
  ┌───────────────┐
  │  Preprocessing │  ← Label mapping, cleaning, scaling
  └───────┬───────┘
          │
    ┌─────┴──────┐
    ▼            ▼
┌────────┐  ┌──────────┐
│  Random│  │ CatBoost │   ← Base classifiers
│ Forest │  │          │
└────┬───┘  └────┬─────┘
     │            │
     └─────┬──────┘
           ▼
   ┌───────────────┐
   │  Meta Features │  ← Probability outputs stacked
   └───────┬───────┘
           ▼
   ┌───────────────────┐
   │ BiLSTM + Attention │  ← Deep meta-classifier
   └───────┬───────────┘
           ▼
   ┌───────────────┐
   │  Final Prediction│
   └───────────────┘
```

---

## 📂 Dataset

**CICIDS2017** — Canadian Institute for Cybersecurity Intrusion Detection Dataset 2017

| File | Day |
|------|-----|
| `Monday-WorkingHours.pcap_ISCX.csv` | Monday (Benign only) |
| `Tuesday-WorkingHours.pcap_ISCX.csv` | Tuesday (FTP-Patator, SSH-Patator) |
| `Wednesday-workingHours.pcap_ISCX.csv` | Wednesday (DoS, Heartbleed) |
| `Thursday-WorkingHours-Afternoon-Infilteration.pcap_ISCX.csv` | Thursday (Infiltration, Web Attacks) |
| `Friday-WorkingHours-Morning.pcap_ISCX.csv` | Friday — **used as Test Set** |

📥 Download from: [https://www.unb.ca/cic/datasets/ids-2017.html](https://www.unb.ca/cic/datasets/ids-2017.html)

---

## 🏷️ Attack Classes

| Label | Attack Types Included |
|-------|----------------------|
| `Normal` | BENIGN traffic |
| `DoS` | DoS Hulk, DoS GoldenEye, DoS slowloris, DDoS |
| `Probe` | PortScan, Bot |
| `BruteForce` | FTP-Patator, SSH-Patator |
| `WebAttack` | Web Attack – Brute Force, XSS, SQL Injection |
| `Other` | Infiltration, Heartbleed |

---

## ⚙️ Installation

### 1. Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/CyberSentry.git
cd CyberSentry
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Place dataset files
Put the CICIDS2017 CSV files inside a `/content/` folder (or update the file paths in the script).

### 4. Run
```bash
python choir_ids.py
```

---

## 📦 Requirements

```
pandas
numpy
matplotlib
seaborn
scikit-learn
catboost
shap
lime
tensorflow
```

---

## 📊 Results

| Metric | Score |
|--------|-------|
| Accuracy | ~99% |
| Precision | ~99% |
| Recall | ~99% |
| F1 Score | ~99% |

> Results may vary slightly based on random seed and dataset sampling.

---

## 📈 Output Plots

| Plot | Description |
|------|-------------|
| `confusion_matrix.png` | Predicted vs True labels across all classes |
| `roc_auc_curve.png` | Per-class ROC curves with AUC scores |
| `calibration_curve.png` | Sigmoid vs Isotonic probability calibration |
| `shap_summary.png` | Top 15 features by SHAP importance |
| `lime_explanation.png` | LIME explanation for a single test instance |

---

## 🔍 Explainability

CyberSentry is built with **trustworthy AI** in mind:

- **SHAP (SHapley Additive exPlanations)** — global feature importance using TreeExplainer on Random Forest
- **LIME (Local Interpretable Model-agnostic Explanations)** — per-instance explanation to understand individual predictions
- **Calibration Curves** — Sigmoid and Isotonic calibration to ensure predicted probabilities are meaningful

---

## 🗂️ Project Structure

```
CyberSentry/
├── choir_ids.py          # Main pipeline script
├── requirements.txt      # Python dependencies
├── README.md             # Project documentation
├── confusion_matrix.png  # Output plot
├── roc_auc_curve.png     # Output plot
├── calibration_curve.png # Output plot
├── shap_summary.png      # Output plot
└── lime_explanation.png  # Output plot
```

---

## 🚀 How It Works

1. **Data Loading** — Five days of CICIDS2017 traffic loaded and merged
2. **Label Mapping** — Raw labels mapped to 6 attack categories
3. **Balanced Sampling** — Up to 5000 samples per class to prevent imbalance
4. **Cleaning** — Infinite values removed, NaNs dropped
5. **Feature Scaling** — StandardScaler applied across all features
6. **Base Model Training** — Random Forest + CatBoost trained independently
7. **Meta Feature Generation** — Probability outputs stacked as input to BiLSTM
8. **BiLSTM + Attention** — Deep meta-classifier trained with early stopping
9. **Evaluation** — Full metrics, plots, SHAP, LIME, and calibration analysis

---

## 👨‍💻 Author

**Your Name**
- GitHub: [@YOUR_USERNAME](https://github.com/YOUR_USERNAME)
- Email: your@email.com

---

## 📄 License

This project is licensed under the **MIT License** — feel free to use, modify, and distribute.

---

## 🙏 Acknowledgements

- [Canadian Institute for Cybersecurity](https://www.unb.ca/cic/) for the CICIDS2017 dataset
- [SHAP](https://github.com/slundberg/shap) by Scott Lundberg
- [LIME](https://github.com/marcotcr/lime) by Marco Tulio Ribeiro
- [CatBoost](https://catboost.ai/) by Yandex

---

> ⭐ If you found this project helpful, please give it a star on GitHub!
