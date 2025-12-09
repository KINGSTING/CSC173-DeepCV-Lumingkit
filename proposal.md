# CSC173 Deep Computer Vision Project Proposal
**Student:** Jemar John J Lumingkit, 2022-1991  
**Date:** 12/10/25

## 1. Project Title 
TubuGAN: Cycle-Consistent Visual Prognosis of Red Rot Disease

## 2. Problem Statement
<div style="text-align: justify">
Sugarcane Red Rot, caused by the fungus Colletotrichum falcatum, is a devastating disease known as the "cancer" of sugarcane, capable of causing up to 100% yield loss if not managed early. While recent advancements in Deep Learning have successfully automated the diagnosis (classification) of the disease, there is a significant lack of tools for prognosis (forecasting severity).
Current diagnostic models typically provide a binary output ("Healthy" or "Diseased") but fail to visualize how the infection will propagate across the leaf surface over time. Furthermore, training prognostic models is difficult because obtaining "paired" temporal data (photographing the exact same leaf at different stages of decay in the wild) is logistically impractical. Consequently, farmers lack the visual data necessary to estimate potential crop degradation, often leading to delayed fungicide application or unnecessary whole-field quarantine. This project addresses the need for a generative simulation tool that can synthesize the future "Severe" state of a leaf from a "Mild" input using unpaired data.
</div>

## 3. Objectives
**General Objective:**
<div style="text-align: justify">
To develop a Deep Learning-based visual prognosis system using CycleGAN that generates synthetic images simulating the progression of Red Rot disease from mild to severe stages.
</div>

**Specific Objectives:**
- **To Implement Automated Domain Sorting:** To develop a Computer Vision algorithm using HSV color space masking to calculate the "Infection Ratio" (diseased pixels vs. total leaf pixels) and automatically partition the dataset into "Mild" (<12% infection) and "Severe" domains.
- **To Train a Generative Model:** To design and train a Cycle-Consistent Generative Adversarial Network (CycleGAN) with ResNet generators to learn the mapping between mild and severe domains without paired training examples.
- **To Evaluate Visual Prognosis:** To create an inference pipeline that accepts real-world mild infection images and outputs high-fidelity synthetic visualizations of the predicted severe necrotic state.

## 4. Dataset Plan
- Source: Kaggle: [Sugarcane Leaf Disease Dataset](https://www.kaggle.com/datasets/nirmalsankalana/sugarcane-leaf-disease-dataset) (~160MB)
- Classes: 
    - Domain A (Input): Red_Rot_Mild (Leaves with small, isolated lesions).
    - Domain B (Target): Red_Rot_Severe (Leaves with large necrosis and coalesced spots).
- Acquisition & Preprocessing:
    - Download public dataset via Kaggle API.
    - Manual Stratification: Since the dataset is labeled by Type (e.g., Red Rot) but not Severity, I will manually filter the "Red Rot" folder into two new sub-folders: "Mild" (early stage) and "Severe" (late stage) to create the unpaired domains required for CycleGAN.

## 5. Technical Approach
- Architecture: CycleGAN (Unpaired Image-to-Image Translation).
    - Generator (G): ResNet-based generator to transform Domain A (Mild) -> Domain B (Severe).
    - Discriminator (D): PatchGAN classifier to distinguish between real severe images and generated ones.
    - Loss Function: Cycle Consistency Loss (L1) + Adversarial Loss (MSE).
- Framework: PyTorch (chosen for superior support of GAN libraries like torch-gan).
- Hardware: Google Colab (T4 GPU)

## 6. Expected Challenges & Mitigations

**Challenge 1:** Mode Collapse (The generator produces the exact same "severe" pattern for every input leaf).
> **Solution 1:** Implement Identity Loss to force the generator to preserve the original leaf shape and background, changing only the disease features.

**Challenge 2:** Subjective Data Labels (Defining "Mild" vs "Severe" is prone to human error).
> **Solution 2:** Use a "Percentage of Infection" (PI) thresholding algorithm (using OpenCV color segmentation) to automatically sort images into domains instead of relying purely on manual guessing.