# 🧠 BraTS 2020: Brain Tumor Segmentation, Data Generation & Survival Prediction

This repository implements a full pipeline for **brain tumor segmentation**, **synthetic MRI generation**, and **overall survival prediction** using the **BraTS 2020 dataset**. It combines deep learning (3D U-Net & CVAE) with traditional ML (Random Forest/XGBoost) for comprehensive glioma analysis.

* **3D U-Net** for tumor segmentation
* **3D CVAE** for data generation
* **Survival Prediction** using extracted radiomic and volumetric features,

---

## 📌 Features

* ✅ **3D U-Net** for volumetric tumor segmentation (WT, TC, ET)
* ✅ **3D CVAE** to generate synthetic 3D MRI volumes conditioned on tumor masks
* ✅ **Survival prediction model** using radiomic, volumetric, and clinical features
* ✅ Designed for low-data settings with augmentation + transfer learning support
* ✅ Evaluation metrics and visualizations for all stages

---

## 🗂️ Project Structure

```
brats20-3dunet-3dautoencoder/
├── data/
│   ├── BraTS2020_TrainingData/
│   └── processed/
├── models/
│   ├── unet3d.py            # U-Net architecture
│   ├── cvae3d.py            # Conditional 3D VAE
│   └── survival_model.py    # ML pipeline for survival
├── utils/
│   ├── dataloader.py
│   ├── metrics.py
│   └── preprocessing.py
├── notebooks/
│   └── brats20-main.ipynb
├── requirements.txt
└── README.md
```

---

## 📥 Dataset

* **Source**: [BraTS 2020 Challenge](https://www.med.upenn.edu/cbica/brats2020/data.html)
* **Modalities**: FLAIR, T1, T1ce, T2
* **Tasks**: Tumor segmentation (labels: WT, TC, ET), overall survival (OS) prediction

---

## 📈 Tasks & Models

### 🧠 1. Tumor Segmentation (3D U-Net)

```python
from models.unet3d import UNet3D
model = UNet3D(in_channels=4, out_channels=3)
```

* Inputs: 4 MRI modalities (240×240×155)
* Output: Multiclass segmentation (WT, TC, ET)
* Loss: Dice + Cross-Entropy
* Metrics: Dice coefficient (per tumor class)

### 📊 2. Synthetic Data Generation (3D CVAE)

```python
from models.cvae3d import CVAE3D
model = CVAE3D(input_shape=(240, 240, 96), num_classes=3, latent_dim=256)
```

* Conditioned on: Tumor masks
* Output: 3D MRI-like volumes for augmentation
* Applications: Boost segmentation performance in low-data regimes

### ⚰️ 3. Survival Prediction

```python
from models.survival_model import train_survival_model
```

* Features: Tumor volume (from segmentation), location stats, patient age
* Models: Random Forest, XGBoost, Ridge Regression
* Labels: Survival days (regression) or class (short/mid/long survivor)
* Evaluation: MAE, R², or classification metrics (F1, accuracy)

---

## 🧪 Evaluation

| Task                | Metric                    |
| ------------------- | ------------------------- |
| Segmentation        | Dice (WT, TC, ET)         |
| Generation          | Reconstruction loss, SSIM |
| Survival Prediction | MAE, Accuracy, F1 Score   |

---

## 📊 Visualizations

* MRI volume slices with overlayed segmentations
* Synthetic MRI vs. real MRI comparisons
* Survival prediction feature importance
* Confusion matrix for survival class prediction

---

## 💻 Getting Started

### ✅ Install Dependencies

```bash
pip install -r requirements.txt
```

Or manually:

```bash
pip install torch torchvision nibabel scikit-learn pandas xgboost matplotlib opencv-python tqdm
---

## 💡 Applications

* Data-efficient tumor segmentation
* Simulated MRI scans for data augmentation
* Predictive modeling for patient outcomes
* Clinical decision support for brain tumor prognosis

---

## 📌 Future Improvements

* Patch-wise training for large-volume scalability
* Attention U-Net variants
* GAN-based realistic synthesis
* Integration with clinical metadata (resection status, MGMT, etc.)

---

## 📄 License

This project is for academic research under the MIT License.

---
