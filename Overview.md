## 🧠 Multimodal Brain Tumor Segmentation and Survival Prediction

This project integrates **3D Deep Learning** and **Statistical Machine Learning** to perform **tumor segmentation**, **feature extraction**, and **survival prediction** from multimodal MRI scans.

---

### 📋 Project Overview

| **Phase**                         | **Goal**                                                                                                                                                                                                                                                                                        | **Model & Method**                                                                                                                                          | **Key Results & Details**                                                                                                                                                                                                                           |   |                                                                                         |
| --------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | - | --------------------------------------------------------------------------------------- |
| **I. Data & Problem**             | **Input:** Multimodal Brain Scans – T1, T1-Gd (T1ce), T2, T2-FLAIR NIfTI files.<br>**Target Labels:** Segmentation regions – NCR/NET (1), ED (2), ET (4), combined into:<br>• Whole Tumor (WT)<br>• Tumor Core (TC)<br>• Enhancing Tumor (ET)<br>**Clinical Data:** Age and Survival Days (SD). | Data preprocessing, normalization, and splitting via **Stratified K-Fold** based on Age.                                                                    | Ensures balanced folds across age groups for reliable generalization.                                                                                                                                                                               |   |                                                                                         |
| **II. Tumor Segmentation**        | **Automatic segmentation** of tumor sub-regions (WT, TC, ET).                                                                                                                                                                                                                                   | **Model:** 3D U-Net with Group Normalization.<br>**Loss:** BCE + Dice Loss.<br>**Metrics:** Dice Coefficient (F1-score), Jaccard Index (IoU).               | **Validation Performance:**<br>• WT: 92.5% / 86.5%<br>• TC: 84.8% / 75.3%<br>• ET: 77.2% / 66.0%<br>Visual outputs show clear 3D tumor mask generation (Ground Truth vs. Prediction).                                                               |   |                                                                                         |
| **III. Feature Extraction**       | **Dimensionality reduction** to extract latent, high-level features for survival and age prediction.                                                                                                                                                                                            | **Model:** 3D AutoEncoder (Convolutional Encoder–Decoder with MaxPooling/Unpooling).<br>**Loss:** Mean Squared Error (MSE).                                 | The encoder compresses the 4×240×240×150 input into a **512-dimensional latent vector**.<br>Combined with **voxel statistical features** (skewness, kurtosis, data distribution for T1, T2, FLAIR, T1ce) to form a **tabular dataset** per patient. |   |                                                                                         |
| **IV. Survival / Age Prediction** | Predict **Age** and **Survival Days (SD)** from extracted features.                                                                                                                                                                                                                             | **Model:** Support Vector Regression (SVR).<br>**Method:** 7-Fold Cross-Validation.<br>**Metric:** Custom Score →  (\text{score} = \frac{1}{n} \sum_{i=1}^n | y_{true,i} - y_{pred,i}                                                                                                                                                                                                                             | ) | Captures the correlation between radiomic + deep latent features and clinical outcomes. |

---

### 🧩 **Tech Stack**

* **Deep Learning:** TensorFlow / Keras
* **Medical Imaging:** Nibabel, NiLearn, OpenCV
* **Machine Learning:** scikit-learn (SVR, Stratified K-Fold)
* **Visualization:** Matplotlib, Seaborn, Plotly
* **Data Format:** NIfTI (.nii.gz)

---

### 📈 **Key Highlights**

* Multi-phase pipeline combining **3D segmentation**, **latent feature learning**, and **clinical prediction**.
* Strong segmentation performance with **92% Dice** on Whole Tumor regions.
* Effective feature compression (512-D latent space) for downstream prediction tasks.
* Interpretable connection between MRI-derived features and patient outcomes.
