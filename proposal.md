
# CSC173 Deep Computer Vision Project Proposal
**Student:** Jemar John J Lumingkit, 2022-1991  
**Date:** 12/10/25

## 1. Project Title 
SugarGuard: A Hybrid Computer Vision Framework for Sugarcane Disease Classification and Precision Severity Estimation

## 2. Problem Statement
Sugarcane farming is a critical economic driver, yet yield is frequently devastated by fungal and viral diseases like Red Rot and Mosaic. Current manual inspection methods are subjective, labor-intensive, and often fail to quantify infection severity accurately, leading to either delayed treatment or excessive pesticide use. This project addresses the need for an automated, precision-agriculture tool that not only identifies the disease type but also provides a quantitative severity assessment to guide specific intervention strategies.

## 3. Objectives
- Develop a robust classifier: Train a Deep Learning model to classify sugarcane leaf images into 5 categories (Healthy, Mosaic, RedRot, Rust, Yellow) with >90% accuracy.
- Implement "Smart" Severity Grading: Engineer a secondary Computer Vision pipeline using Instance Segmentation to isolate leaves from complex backgrounds (soil, debris) and calculate precise infection percentages.
- Create a Self-Correcting Pipeline: Integrate the classification and segmentation models into a unified system that cross-verifies results to eliminate false positives (e.g., mistaking soil for disease).

## 4. Dataset Plan
- Source: Kaggle: [Sugarcane Leaf Disease Dataset](https://www.kaggle.com/datasets/nirmalsankalana/sugarcane-leaf-disease-dataset) (~160MB)
- Classes: 1. Healthy 2. Mosaic 3. RedRot 4. Rust 5. Yellow
- Acquisition: Automated download via kagglehub API in Google Colab to ensure reproducibility and easy access to the latest version.

## 5. Technical Approach
- Architecture: A Hybrid Two-Stage Pipeline:
    - Stage 1 (Diagnosis): A Convolutional Neural Network (CNN) analyzes the global context of the image to predict the disease class.
    - Stage 2 (Quantification): A Logic-Gated Segmentation module isolates the specific leaf and performs spectral analysis to measure the diseased area.
- Model: Classification: MobileNetV2 (Transfer Learning from ImageNet) for lightweight, high-accuracy disease recognition.
    - Segmentation: FastSAM (Fast Segment Anything Model) for Instance Segmentation to remove background noise (soil/sky).
- Framework: TensorFlow/Keras (for MobileNetV2 training/inference).
    - PyTorch/Ultralytics (for FastSAM segmentation).
    - OpenCV (for HSV color thresholding and contour analysis).
- Hardware: Google Colab (T4 GPU)

## 6. Expected Challenges & Mitigations
- Challenge 1: Small Dataset (Overfitting) Mitigation: Utilization of Transfer Learning (freezing MobileNetV2 base layers) and aggressive Data Augmentation (rotation, zoom, shear) to artificially expand the training set.
- Challenge 2: Background Noise (False Positives) Mitigation: Standard classifiers often mistake background soil for disease. I will implement Instance Segmentation (FastSAM) to computationally "erase" the background before severity analysis, ensuring only leaf pixels are counted.
- Challenge 3: Distinguishing "Yellow Leaf" from Natural Senescence Mitigation: Implementation of a Logic Gate (Auto-Correction). If the classifier predicts a disease but the severity calculator finds <1.5\% infection (trace noise), the system will automatically override the diagnosis to "Healthy."