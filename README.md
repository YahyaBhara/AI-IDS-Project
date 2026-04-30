# AI-Based Intrusion Detection System (IDS)

> **Building upon:** Awajan, A. (2023). *A Novel Deep Learning-Based Intrusion Detection System for IoT Networks.* Computers, 12(2), 34.

---

## Overview

This project implements and compares three machine learning models for network intrusion detection using the NSL-KDD dataset. It builds directly upon Awajan (2023) by:

1. **Replicating** the paper's FCFFN architecture on a standardized benchmark dataset
2. **Addressing** the dataset limitation the paper identifies in Section 5.3 — using NSL-KDD instead of a single-network custom dataset
3. **Providing** the missing model comparison the paper acknowledges in Section 5.2
4. **Extending** the paper's single-model approach with a baseline comparison

All three models classify network traffic as **Normal** or **Attack**.

---

## Models

| # | Model | Description |
|---|-------|-------------|
| 1 | **Logistic Regression** | Baseline classifier |
| 2 | **Neural Network (MLP)** | Our primary deep learning model |
| 3 | **FCFFN — Paper Architecture** | Replication of Awajan (2023), Section 3.2.3 — 5 hidden layers, ReLU, SGD optimizer |

---

## Results

Results on NSL-KDD test set (30% split, 125,973 total records):

| Model | Accuracy | Precision | Recall | F1-Score |
|-------|----------|-----------|--------|----------|
| Logistic Regression (Ours) | 93.14% | 95.39% | 89.50% | 92.35% |
| Neural Network MLP (Ours) | 95.44% | 95.42% | 94.70% | 95.06% |
| FCFFN Replicated (Paper Arch.) | 95.31% | 94.97% | 94.90% | 94.93% |
| **Paper Reported — Awajan (2023)** | **93.74%** | **93.71%** | **93.82%** | **93.47%** |

Our replicated FCFFN outperforms the paper's reported results across all metrics when trained on the more diverse NSL-KDD dataset, supporting the paper's own argument in Section 5.3 that dataset diversity is key to a generalizable IDS.

---

## Attack Type Demo

The final notebook cell simulates sample traffic for each of the **5 attack types from the paper's intrusion model (Section 4.1)** and tests how all three models classify them:

| Traffic Type | Log. Reg. | NN MLP | Paper FCFFN |
|---|---|---|---|
| Normal Traffic | NORMAL | NORMAL | NORMAL |
| Blackhole Attack (BHA) | NORMAL | NORMAL | NORMAL |
| DDoS Attack | ATTACK | ATTACK | ATTACK |
| Opportunistic Service (OSA) | ATTACK | ATTACK | ATTACK |
| Sinkhole Attack (SHA) | NORMAL | NORMAL | NORMAL |
| Wormhole Attack (WHA) | NORMAL | NORMAL | NORMAL |

> **Note:** Blackhole, Sinkhole, and Wormhole are IoT routing-layer attacks not present in NSL-KDD. All models classifying them as Normal is itself a meaningful finding — it demonstrates the dataset generalization limitation the paper raises in Section 5.3, showing that a model trained on one network's traffic patterns will not cover all attack types.

---

## Features

The 8 features used map directly to the paper's feature set (Table 1, Section 3.2.2):

| Our Feature (NSL-KDD) | Paper Equivalent |
|---|---|
| `src_bytes` | Transmission Rate (Tr) |
| `dst_bytes` | Reception Rate (Rr) |
| `flag` | Transmission Mode (Tm) |
| `logged_in` | Active Session (As) |
| `same_srv_rate` | Normal bandwidth pattern |
| `diff_srv_rate` | Anomalous service switching |
| `serror_rate` | DoS/DDoS indicator |
| `count` | Anomalous volume indicator |

---

## How to Run

**1. Clone the repository**
```bash
git clone https://github.com/YahyaBhara/AI-IDS-Project.git
cd AI-IDS-Project
```

**2. Install dependencies**
```bash
pip install -r requirements.txt
```

**3. Update the data path**

Open `code_final.ipynb` and update `DATA_PATH` in Cell 1 to point to your local copy of `KDDTrain+.txt`:
```python
DATA_PATH = "/your/path/to/KDDTrain+.txt"
```

**4. Run the notebook**

Open `code_final.ipynb` and run all cells in order.

---

## Dataset

- **NSL-KDD** — improved version of the KDD Cup 1999 dataset
- File: `KDDTrain+.txt` — included in the `data/` folder
- 125,973 records | ~53.7% normal | ~46.3% attack
- Covers 4 attack categories: DoS, Probe, R2L, U2R

---

## Project Structure

```
AI-IDS-Project/
├── code_final.ipynb      # Main notebook — all models + comparison + demo
├── data/
│   └── KDDTrain+.txt     # NSL-KDD training dataset
├── requirements.txt
└── README.md
```

---

## Tech Stack

- Python 3.9+
- Pandas, NumPy
- Scikit-learn
- Matplotlib, Seaborn
- Jupyter Notebook

---

## Limitations

- Binary classification only (Normal vs Attack) — paper classifies 5 specific attack types
- NSL-KDD does not contain IoT routing-layer attacks (Blackhole, Sinkhole, Wormhole)
- FCFFN replication uses `MLPClassifier` — exact paper weights and architecture cannot be fully reproduced without the original training data
- Not deployed as a real-time system

---

## References

- Awajan, A. (2023). A Novel Deep Learning-Based Intrusion Detection System for IoT Networks. *Computers, 12*(2), 34. https://doi.org/10.3390/computers12020034
- Tavallaee, M., et al. (2009). A Detailed Analysis of the KDD CUP 99 Data Set. *IEEE Symposium on Computational Intelligence for Security and Defense Applications.*


