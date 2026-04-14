# Step 1: Pre-screening Model Training

## Objective
Training a fast scanner based on MobileNetV2 to filter out empty and non-cellular regions in pathology slides.

## Configuration & Hyperparameters
| Parameter | Value |
|:---|:---|
| Base Model | MobileNetV2 (Pre-trained ImageNet) |
| Patch Size | 224 × 224 |
| Scan Level | 2 |
| Cellularity Threshold | 3% |
| Training Patients | 80 |
| Patches per Patient | 50 |
| Epochs | 30 |
| Batch Size | 32 |
| Random Seed | 42 (Deterministic & Reproducible) |

## Results
| Metric | Value |
|:---|:---|
| Fold 1 Validation Accuracy | 92.47% |
| Fold 2 Validation Accuracy | 94.29% |
| Fold 3 Validation Accuracy | 93.84% |
| Fold 4 Validation Accuracy | 94.52% |
| Fold 5 Validation Accuracy | 94.74% |
| **5-Fold Cross-Validation Mean** | **93.97% ± 0.81%** |
| **Accuracy on Test Patients** | **79.75%** |

## Dataset Information
| Item | Value |
|:---|:---|
| Total Slides in Step 1 | 100 |
| Training Slides | 80 |
| Test Slides | 20 |
| **Note** | **These 100 slides are exclusively used for scanner training and evaluation. A completely separate cohort of slides is used in subsequent steps (Step 2-4) to ensure independent validation and avoid data leakage.** |

## Outputs of This Step
| File | Description |
|:---|:---|
| `scanner_model_trained_improved.h5` | Trained model weights |
| `step1_results_improved.pkl` | Complete cross-validation results |
| `step1_log_improved.txt` | Execution log |

## Full Report (PDF)
[Download and view Step 1 detailed report](../pdfs/Step1.output.pdf)

---

[Back to Home](../README.md)
