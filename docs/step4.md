# Step 4: ABMIL Training & Clinical Interpretation

## Objective
Training an Attention-based Multiple Instance Learning (ABMIL) model on H-optimus-0 features for slide-level breast cancer classification, with patient-level data split to prevent leakage, and generating interpretable attention heatmaps.

## Configuration & Hyperparameters
| Parameter | Value |
|:---|:---|
| Model Architecture | ABMIL (Attention-based MIL) |
| Feature Dimension | 1,536 (H-optimus-0) |
| Hidden Dimension | 512 |
| Dropout | 0.6 |
| Learning Rate | 0.0001 |
| Weight Decay | 3e-3 |
| Epochs | 50 (with Early Stopping) |
| Early Stopping Patience | 8 |
| Min Epochs | 15 |
| Cross-Validation Folds | 5 |
| Train/Validation Split | 70% / 30% (Patient-Level) |

## Dataset Information
| Item | Value |
|:---|:---|
| Total Training Slides (from Step 3) | 200 |
| Total Training Patients | 151 |
| Malignant Patients | 89 |
| Benign Patients | 62 |
| Train Slides (70%) | 137 (from 105 patients) |
| Validation Slides (30%) | 63 (from 46 patients) |
| External Test Slides | 86 |
| **Note** | **Patient-level split ensures NO DATA LEAKAGE. All slides from a single patient are assigned entirely to either train or validation set. The 86 test slides are a completely external cohort, never used in any previous step (Step 1, 2, or 3).** |

## Cross-Validation Results (5-Fold on Train Slides)
| Fold | Validation Accuracy |
|:---|:---|
| Fold 1 | 100.00% |
| Fold 2 | 96.43% |
| Fold 3 | 92.59% |
| Fold 4 | 96.30% |
| Fold 5 | 92.59% |
| **Mean ± Std** | **95.58% ± 2.78%** |

## Final Model Results
| Metric | Value |
|:---|:---|
| Final Model Validation Accuracy | 95.24% |
| **External Test Accuracy** | **90.70%** |
| **External Test Precision** | **91.23%** |
| **External Test Recall (Sensitivity)** | **94.55%** |
| **External Test F1-Score** | **0.929** |
| **External Test AUC-ROC** | **0.975** |
| **AUC 95% Confidence Interval** | **[0.937, 0.997]** |

## Confusion Matrix (External Test)
| | Predicted Benign | Predicted Malignant |
|:---|:---:|:---:|
| **Actual Benign** | TN = 26 | FP = 5 |
| **Actual Malignant** | FN = 3 | TP = 52 |

## Interpretation & Heatmaps
| Item | Value |
|:---|:---|
| Heatmaps Generated | 86 (all external test slides) |
| Method | Attention weights from ABMIL overlaid on WSI |
| Interpretation | Red = High attention (tumor regions), Blue = Low attention (normal tissue) |

## Outputs of This Step
| File | Description |
|:---|:---|
| `final_abmil_model.pth` | Trained ABMIL model weights |
| `final_results.pkl` | Complete evaluation metrics |
| `model_predictions.pkl` | Predictions for all test slides |
| `all_heatmaps.zip` | Attention heatmaps for 86 test slides |
| `heatmap_report.pkl` | Detailed heatmap metadata |

## Full Report (PDF)
[Download and view Step 4 detailed report](../pdfs/Step4.output.pdf)

---

[Back to Home](../README.md)
