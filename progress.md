# CSC173 Deep Computer Vision Project Progress Report
**Student:** Jemar John J Lumingkit, 2022-1991  
**Date:** 12/10/25  
**Repository:** [https://github.com/KINGSTING/CSC173-DeepCV-Lumingkit](https://github.com/KINGSTING/CSC173-DeepCV-Lumingkit)  
**Commits Since Proposal:** [11 commits] | **Last Commit:** [12/09/25]

## 📊 Current Status
| Milestone | Status | Notes |
|-----------|--------|-------|
| Dataset Preparation | ✅ Completed | 3,108 images sorted via HSV algorithm |
| Initial Training | 🟡 In Progress| Pipeline verified via CPU debug; GPU run pending |
| Baseline Evaluation | ⏳ Pending | Awaiting full training weights |
| Model Fine-tuning | ⏳ Not Started | Planned for post-training analysis |

## 1. Dataset Progress
- **Total images:** 3,108 images (Sugarcane Red Rot)
- **Domain Split:** 
    - **Domain A (Mild):** 718 images (<12% infection ratio)
    - **Domain B (Severe):** 2,390 images (≥12% infection ratio)
- **Preprocessing applied:**
    - HSV Color Masking for automated severity sorting.
    - Resize to 256 x 256.
    - Normalization (mean=[0.5], std=[0.5]).

**Sample data preview:**
> Note: Dataset successfully separated into dataset_prognosis/mild and dataset_prognosis/severe directories.

## 2. Training Progress

**Training Curves (Initial Debug Run)**
![Loss Curve](images/loss_curve.png)


**Current Metrics (Epoch 1 - Debug Mode):** Note: Metrics below reflect the Generative Adversarial Network performance, not classification accuracy.
| Metric | Value | Interpretation |
|--------|-------|-----|
| Loss_G (Generator) | [0.45] | High initial error (expected at start); includes Cycle + Identity loss. |
| Loss_D (Discriminator)| [0.38] | Discriminator is easily detecting fakes currently. |
| Cycle Consistency | [2.10] | Model is learning to preserve leaf shape structure. |

## 3. Challenges Encountered & Solutions
| Issue | Status | Resolution |
|-------|--------|------------|
| Google Colab GPU Limit | ✅ Fixed | Implemented a "Fast Debug" CPU mode (1 epoch, 5 batches) to verify code logic before full training. |
| Unpaired Data Sorting | ✅ Fixed | Created an automated OpenCV algorithm to calculate "Infection Ratio" and split folders automatically. |
| Training Speed | ⏳ Ongoing | Code optimized with torch.amp (Mixed Precision); waiting for T4 GPU availability for full run. |

## 4. Next Steps (Before Final Submission)
- [ ] **Full Training:** Execute 50-100 epochs on T4 GPU once quota resets.
- [ ] **Inference Pipeline:** Generate side-by-side comparisons (Original Mild vs. Generated Severe) for the final report.
- [ ] **Evaluation:** Calculate SSIM (Structural Similarity Index) to ensure leaf structure is preserved.
- [ ] **Documentation:** Record 5-min demo video showing the "Upload -> Prognosis" workflow.
- [ ] **Final Polish:** Update README.md with generated sample images.
