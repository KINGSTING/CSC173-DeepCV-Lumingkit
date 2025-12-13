# CSC173 Deep Computer Vision Project Progress Report
**Student:** Jemar John J Lumingkit, 2022-1991  
**Date:** 12/10/25  
**Repository:** [https://github.com/KINGSTING/CSC173-DeepCV-Lumingkit](https://github.com/KINGSTING/CSC173-DeepCV-Lumingkit)  
**Commits Since Proposal:** [15 commits] | **Last Commit:** [12/13/25]

## 📊 Project Status: COMPLETED
| Milestone | Status | Notes |
|-----------|--------|-------|
| Dataset Preparation | ✅ Completed | 3,108 images sorted via HSV algorithm |
| Model Architecture | ✅ Completed | CycleGAN with Replay Buffer & ResNet Generator |
| Stability Optimization| ✅ Completed | Implemented Replay Buffer & Checkpoint Resume Logic |
| Full Training | ✅ Completed | 50 Epochs executed on Kaggle T4 GPU |
| Final Evaluation | ✅ Completed | SSIM calculation & Inference Demo finalized |

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

**Training Curves**
![Training Curve](https://drive.google.com/uc?export=view&id=1NRnPqbRpHMKLJu2MYqSrV4AxPDbERTFL)


**Current Metrics (Epoch 1 - Debug Mode):** Note: Metrics below reflect the Generative Adversarial Network performance, not classification accuracy.
| Metric | Value | Interpretation |
|--------|-------|-----|
| Loss_G (Generator) | [0.45] | High initial error (expected at start); includes Cycle + Identity loss. |
| Loss_D (Discriminator)| [0.38] | Discriminator is easily detecting fakes currently. |
| Cycle Consistency | [2.10] | Model is learning to preserve leaf shape structure. |

## 3. Challenges Encountered & Solutions
| Issue | Status | Resolution |
|-------|--------|------------|
| **Mode Collapse / Instability** | ✅ Fixed | The standard training loop was unstable. Implemented a **Replay Buffer** (Shrivastava et al., 2017) to stabilize the discriminator updates. |
| **Runtime Disconnects (Kaggle)**| ✅ Fixed | Implemented a robust `save_checkpoint` system that auto-saves "Latest" and "Permanent" weights, combined with logic to auto-detect and resume from the last epoch. |
| **Unpaired Data Sorting** | ✅ Fixed | Created an automated OpenCV algorithm to calculate "Infection Ratio" and split folders automatically based on a 12% threshold. |
| **Visualization Errors** | ✅ Fixed | Corrected tensor denormalization logic to properly display High-Dynamic Range (HDR) tensors as viewable RGB images. |

## 4. Final Deliverables
- [x] **Full Training:** 50-epoch run completed on Kaggle T4.
- [x] **Inference Pipeline:** Generated side-by-side comparisons (Original Mild vs. Generated Severe).
- [x] **Video Presentation:** Recorded 5-minute technical walkthrough covering "Problem -> CycleGAN Architecture -> Results".
- [x] **Documentation:** README.md updated with sample prognosis images and deployment instructions.
