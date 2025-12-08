# 🌾 Sugarcane Leaf Disease Detection using CNN

A Deep Learning project that utilizes **Computer Vision (Convolutional Neural Networks)** to automatically detect and classify various diseases in sugarcane leaves. This tool aims to assist farmers and agricultural researchers in early disease diagnosis to prevent crop loss.

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange)
![Google Colab](https://img.shields.io/badge/Platform-Google%20Colab-yellow)

## 📌 Project Overview
Sugarcane is a major industrial crop, but it is susceptible to various fungal and viral diseases. Manual inspection of leaves is time-consuming and prone to error.

This project implements a **Convolutional Neural Network (CNN)** to classify leaf images into **5 distinct categories** based on visual symptoms (spots, stripes, and discoloration).

## 🍃 Disease Classes
The model is trained to identify the following conditions:
1.  **Healthy** (No disease)
2.  **Mosaic** (Characterized by yellow/green mottling or stripes)
3.  **Red Rot** (Bright red lesions on the midrib)
4.  **Rust** (Orange/brown pustules on the leaf surface)
5.  **Yellow** (General yellowing/chlorosis)

## 📂 Dataset Details
* **Source:** [Sugarcane Leaf Disease Dataset (Kaggle)](https://www.kaggle.com/datasets/nirmalsankalana/sugarcane-leaf-disease-dataset)
* **Data Structure:**
    * Input Shape: `150x150` pixels
    * Format: RGB Images
* **Data Augmentation:** The model uses `ImageDataGenerator` for rotation, zooming, and shearing to improve generalization.

## 🧠 Model Architecture
The project uses a custom Sequential CNN built with **TensorFlow/Keras**:
* **4 Convolutional Layers:** To extract features like edges, textures (stripes/spots), and shapes.
* **MaxPooling Layers:** To reduce dimensionality and computation.
* **Flatten Layer:** To convert 2D feature maps to a 1D vector.
* **Dropout Layer (0.5):** To prevent overfitting during training.
* **Dense Output Layer:** Softmax activation for multi-class classification (5 classes).

## 🚀 How to Run (Google Colab)
This project is optimized for Google Colab. No manual download of the dataset is required (it uses `kagglehub`).

1.  **Open the Notebook:** Upload the `.ipynb` file to Google Drive.
2.  **Open with Google Colab:** Right-click the file > Open with > Google Colaboratory.
3.  **Run All Cells:**
    * The script will automatically download the dataset from Kaggle.
    * It will preprocess the images and train the model.
4.  **Test Your Own Image:**
    * Scroll to the "Upload & Predict" section at the bottom.
    * Run the cell and click **"Choose Files"** to upload a photo of a sugarcane leaf.
    * The model will output the diagnosis and confidence score.

## 📊 Results & Visualization
The notebook includes visualization tools to evaluate performance:
* **Accuracy & Loss Graphs:** Tracks model learning over epochs.
* **Confusion Matrix:** A heatmap showing exactly which diseases the model confuses (e.g., RedRot vs. Rust).
* **Prediction Confidence:** Displays percentage certainty for predictions.

## 🛠️ Tech Stack
* **Language:** Python 3
* **Deep Learning:** TensorFlow, Keras
* **Data Processing:** NumPy, Pandas
* **Visualization:** Matplotlib, Seaborn
* **Data Source:** KaggleHub

## 📜 Citations
If you use this project or the dataset, please credit the original dataset providers:
* *Dataset:* Sugarcane Leaf Disease Dataset by Nirmal Sankalana (Kaggle).
* *Original Research:* Daphal, Swapnil; Koli, Sanjay (2019).

---
**Author:** Jemar John J Lumingkit  
**University:** Mindanao State University - Iligan Institute of Technology  
**Date:** December 2025
