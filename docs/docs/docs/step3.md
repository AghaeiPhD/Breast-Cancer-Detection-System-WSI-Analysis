# Step 3: Targeted Patch & Feature Extraction

## Objective
Extracting high-resolution patches from suspicious regions identified in Step 2 and computing deep features using the H-optimus-0 foundation model for subsequent MIL classification.

## Configuration & Hyperparameters
| Parameter | Value |
|:---|:---|
| Feature Extractor | H-optimus-0 (bioptimus/H-optimus-0) |
| Feature Dimension | 1,536 |
| Patches per Slide | 200 |
| Regions per Slide | 40 |
| Patches per Region | 5 |
| Target Patch Size | 224 × 224 |
| Batch Size | 16 |
| Device | Tesla P100-PCIE-16GB |

## Dataset Information
| Item | Value |
|:---|:---|
| Total Slides Processed | 200 |
| Slides with Patches | 200 |
| Total Unique Patients | 151 |
| Slides per Patient (Min / Max / Avg) | 1 / 5 / 1.3 |
| **Note** | **These 200 slides are the same cohort used in Step 2 (independent from Step 1). Patient-level metadata is preserved for proper data splitting in Step 4.** |

## Results
| Metric | Value |
|:---|:---|
| Total Patches Extracted | 40,000 |
| Feature Matrix Shape | (40,000 × 1,536) |
| GPU Memory Allocated | 4.27 GB |
| Features File Size | 235.0 MB |
| Patches File Size | 5,745.9 MB |

## Outputs of This Step
| File | Description |
|:---|:---|
| `features_for_abmil.pkl` | Feature vectors + slide filenames + patient IDs + coordinates |
| `all_patches.pkl` | All extracted patches + coordinates + metadata (for heatmaps) |

## Full Report (PDF)
[Download and view Step 3 detailed report](../pdfs/Step3.output.pdf)

---

[Back to Home](../README.md)
