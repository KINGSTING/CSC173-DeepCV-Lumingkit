
# CSC173 Deep Computer Vision Project Proposal
**Student:** Jemar John J Lumingkit, 2022-1991  
**Date:** 12/10/25

## 1. Project Title 
SugarGuard: Automated Sugarcane Leaf Disease Classification Using Deep Transfer Learning

## 2. Problem Statement
Sugarcane is a vital industrial crop, but its yield is frequently compromised by fungal and viral diseases such as Red Rot and Mosaic, which are difficult to distinguish visually in early stages. Manual inspection by farmers is labor-intensive, subjective, and prone to error, leading to delayed treatment and economic loss. This project addresses the need for a rapid, automated, and accessible diagnostic tool that enables early intervention and crop protection.

## 3. Objectives
-Develop and train a Convolutional Neural Network (CNN) capable of classifying sugarcane leaves into five distinct categories: Healthy, Mosaic, RedRot, Rust, and Yellow.
-Achieve a validation accuracy of at least 90% by utilizing Transfer Learning techniques to overcome data scarcity.
-Implement a complete pipeline including data augmentation to handle class imbalances and robust validation to ensure real-world applicability.

## 4. Dataset Plan
- Source: Kaggle - Sugarcane Leaf Disease Dataset (~160MB)
- Classes: 1. Healthy 2. Mosaic 3. RedRot 4. Rust 5. Yellow
- Acquisition: Automated download via kagglehub API in Google Colab to ensure reproducibility and easy access to the latest version.

## 5. Technical Approach
- Architecture: Deep Learning with Transfer Learning
- Model: I will utilize a pre-trained backbone (feature extractor) such as MobileNetV2 or EfficientNetB0, which are optimized for efficiency and performance on smaller datasets, followed by custom fully connected layers for the 5-class classification.
- Framework: TensorFlow / Keras
- Hardware: Google Colab (T4 GPU)
- Pipeline:
    - 1. Preprocessing: Resize to 224 x 224, normalization (0-1).
    - 2. Augmentation: Random rotation, zoom, and horizontal flips to increase dataset diversity.
    - 3. Training: Fine-tuning the pre-trained model with a categorical cross-entropy loss function.

## 6. Expected Challenges & Mitigations
- Challenge #1: Overfitting due to the relatively small number of images per class (approx. 500 images/class).
- Solution #1: Apply aggressive data augmentation (shear, zoom, flip) and implement Dropout layers and Early Stopping.
- Challenge #2: Visual Similarity between diseases (e.g., Rust vs. RedRot spots).
- Solution #2: Use a powerful feature extractor (like MobileNetV2 trained on ImageNet) to detect subtle texture differences that a custom CNN might miss.
