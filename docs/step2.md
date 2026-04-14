# Step 2: Suspicious Region Screening

## Objective
Scanning whole slide images with a 50×50 grid to identify suspicious regions using the pre-trained MobileNetV2 scanner from Step 1.

## Configuration & Hyperparameters
| Parameter | Value |
|:---|:---|
| Scanner Model | MobileNetV2 (from Step 1) |
| Grid Size | 50 × 50 |
| Total Patches per Slide | 2,500 |
| Scan Level | 2 |
| Patch Size | 224 × 224 |
| Cellularity Threshold | 3% |
| Suspicious Threshold | 0.5 |
| Max Suspicious Regions per Slide | 40 |
| Random Seed | 42 (from Step 1) |

## Dataset Information
| Item | Value |
|:---|:---|
| Total Slides Scanned | 200 |
| Slides with Suspicious Regions | 200 |
| **Note** | **These 200 slides are completely separate from the 100 slides used in Step 1. This ensures independent validation and prevents data leakage.** |

## Results
| Metric | Value |
|:---|:---|
| Total Patients Scanned | 200 |
| Patients with Suspicious Regions | 200 |
| Total Suspicious Regions Found | 8,000 |
| Average Suspicious Regions per Patient | 40.0 |

## Outputs of This Step
| File | Description |
|:---|:---|
| `phase2_results.pkl` | Coordinates and scores of suspicious regions for all 200 slides |
| `step2_log.txt` | Execution log |

## Full Report (PDF)
[Download and view Step 2 detailed report](../pdfs/Step2.output.pdf)

---

[Back to Home](../README.md)
