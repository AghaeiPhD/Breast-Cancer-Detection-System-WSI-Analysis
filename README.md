# Breast Cancer Detection System - WSI Analysis

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Model: H-optimus-0](https://img.shields.io/badge/Backbone-H--optimus--0-blue)]()
[![Data: TCGA](https://img.shields.io/badge/Data-TCGA-lightgrey)]()

A 4-step computational pathology pipeline for breast cancer detection from whole slide images (WSI). Combines MobileNetV2 pre-screening, H-optimus-0 foundation model features, and attention-based MIL (ABMIL). Includes validation results on TCGA and external cohorts.

---

## Pipeline Overview

```
Step 1: Pre-screening (MobileNetV2) → Filters empty regions (93.97% CV accuracy)
    ↓
Step 2: Grid Scanning (50×50) → Identifies 40 suspicious regions per slide
    ↓
Step 3: Feature Extraction (H-optimus-0) → 1,536-dim features from 200 patches/slide
    ↓
Step 4: ABMIL Classification → Slide-level diagnosis with attention heatmaps
```

---

## Key Results

| Dataset | Slides | AUC-ROC | Accuracy | Sensitivity |
|:---|:---:|:---:|:---:|:---:|
| **TCGA (External Test)** | 86 | **0.975** | **90.70%** | 94.55% |
| **Camelyon (Few-shot)** | 7 | **0.750** | **75.0%** | 100% |

### TCGA Test Set (86 slides)
- **AUC-ROC:** 0.975 (95% CI: 0.937 - 0.997)
- **Accuracy:** 90.70% | **Precision:** 91.23% | **Recall:** 94.55% | **F1:** 0.929
- **Cross-Validation (5-fold):** 95.58% ± 2.78%

### Camelyon External Validation (Few-shot Adaptation)
- Fine-tuned on **only 3 patients**, tested on 4 patients
- **Accuracy improved from 50% → 75%** | **AUC improved from 0.500 → 0.750**
- **100% recall** maintained (no missed malignancies)

---

## Sample Attention Heatmaps

The ABMIL model generates interpretable attention maps showing which regions influenced the diagnosis. **Red areas** indicate high model attention (suspected tumor), **blue areas** indicate low attention (normal tissue). Decision threshold is **0.35** (35%).

| Type | True | Predicted | Probability | File |
|:---|:---:|:---:|:---:|:---|
| True Positive 1 | Malignant | Malignant | 100% | [View](heatmaps/tp_malignant_01.png) |
| True Positive 2 | Malignant | Malignant | 100% | [View](heatmaps/tp_malignant_02.png) |
| True Negative | Benign | Benign | 29.6% | [View](heatmaps/tn_benign_01.png) |
| False Positive | Benign | Malignant | 91.7% | [View](heatmaps/fp_benign_wrong.png) |
| False Negative | Malignant | Benign | 0% | [View](heatmaps/fn_malignant_missed.png) |

### Interpretation

| Sample | What It Shows |
|:---|:---|
| **True Positives (100%)** | Model correctly identified malignant regions with **very high confidence**. Attention maps highlight dense tumor areas. |
| **True Negative (29.6%)** | Model correctly classified benign tissue with **low confidence** (below threshold). Attention is scattered, no clear tumor focus. |
| **False Positive (91.7%)** | Model was **highly confident** but wrong. Likely mistook **inflammation or dense benign tissue** for tumor. This reveals a known limitation of the model. |
| **False Negative (0%)** | Model had **zero confidence** in malignancy and predicted benign, but was wrong. This represents a **missed low-grade or subtle tumor** that the model failed to recognize. |

### Key Takeaways

- **Strengths:** Model is highly confident on clear malignant cases (TP=100%).
- **Limitations:** May confuse inflammation with tumor (FP=91.7%). May miss subtle/low-grade tumors (FN=0%).
- **Clinical Implication:** Model is **conservative** (threshold 0.35), prioritizing high sensitivity. False positives are acceptable in screening; false negatives are the main concern.

---

## Documentation

Detailed technical documentation for each step:

| Step | Description | Link |
|:---:|:---|:---|
| 1 | Pre-screening Model Training (MobileNetV2) | [docs/step1.md](docs/step1.md) |
| 2 | Suspicious Region Screening (50×50 Grid) | [docs/step2.md](docs/step2.md) |
| 3 | Feature Extraction (H-optimus-0) | [docs/step3.md](docs/step3.md) |
| 4 | ABMIL Training & Clinical Interpretation | [docs/step4.md](docs/step4.md) |
| ★ | External Validation (Camelyon - Few-shot) | [docs/validation_external.md](docs/validation_external.md) |

---

## Model Architecture

| Component | Specification |
|:---|:---|
| **Pre-screening** | MobileNetV2 (ImageNet pre-trained) |
| **Feature Extractor** | H-optimus-0 (bioptimus/H-optimus-0) - 1,536 dimensions |
| **MIL Aggregator** | Attention-based MIL (ABMIL) - 512 hidden dims, dropout 0.6 |
| **Decision Threshold** | 0.35 (optimized for high recall) |

---

## Clinical Features

- **Patient-level data split:** NO leakage between train/validation
- **External validation:** Completely independent test set (86 TCGA slides)
- **Cross-dataset testing:** Validated on Camelyon (different scanner/population)
- **Explainable AI:** Attention heatmaps show tumor regions
- **Few-shot adaptation:** Adapts to new domains with only 3 annotated patients

---

## Repository Structure

```
Breast-Cancer-Detection-System-WSI-Analysis/
├── README.md
├── LICENSE
├── .gitignore
├── docs/
│   ├── step1.md
│   ├── step2.md
│   ├── step3.md
│   ├── step4.md
│   └── validation_external.md
├── pdfs/
├── results/
└── heatmaps/
```

---

## Author

**F.P. Aghaei**
- Project Date: March - April 2026
- License: MIT

---

## Citation

If you use this work, please cite:

```
Aghaei, F.P. (2026). Breast Cancer Detection System - WSI Analysis.
A 4-step computational pathology pipeline using H-optimus-0 and ABMIL.
GitHub: https://github.com/AghaeiPhD/Breast-Cancer-Detection-System-WSI-Analysis
```
