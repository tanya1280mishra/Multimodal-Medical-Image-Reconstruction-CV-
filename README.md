# 🧠 Brain Tumor Segmentation & Synthetic Data Generation using 3D U-Net and CVAE

<p align="center">
  <img src="assets/brain_digital.jpg" alt="Digital Brain" width="500"/>
</p>

This project implements a **3D U-Net** for brain tumor segmentation on the **BraTS 2020** dataset and a **3D Conditional Variational Autoencoder (CVAE)** for generating realistic synthetic brain MRI volumes. The goal is to enhance tumor segmentation accuracy and robustness, especially in data-scarce scenarios.

---

## 🔍 Project Objective

- 🧬 **Segment brain tumors** from multi-modal MRI volumes.
- ⚗️ **Generate synthetic 3D brain scans** using a CVAE conditioned on tumor masks.
- 📈 **Augment training data** with realistic samples to improve model generalization.

---

## 📂 Dataset

- **Source**: [BraTS 2020 Challenge](https://www.med.upenn.edu/cbica/brats2020/data.html)
- **Modalities**: T1, T1CE, T2, FLAIR
- **Ground Truth**: Segmentation masks with labels — edema, enhancing tumor, and necrotic tumor

---

## 🏗️ Model Architectures

### 🔹 3D U-Net
- Encoder-decoder structure with skip connections
- Input shape: `240x240x96x4`
- Loss: Dice coefficient + Cross Entropy
- Output: 3 tumor classes

### 🔸 3D CVAE
- Conditional latent space with 3D convolutions
- Conditioned on tumor class masks
- Trained to reconstruct and generate MRI volumes

<p align="center">
  <img src="assets/brain_highlighted.jpg" alt="Brain with Tumor" width="400"/>
  <br/>
  <em>Figure: Visualizing tumor regions from segmentation output</em>
</p>

---

## 💻 Tech Stack

| Component       | Details                             |
|----------------|-------------------------------------|
| Framework      | TensorFlow / Keras                  |
| Language       | Python                              |
| Visualization  | Matplotlib, Seaborn                 |
| Data Handling  | nibabel, NumPy                      |
| Metrics        | Dice Score, Accuracy, Reconstruction Loss |

---

## 🚀 How to Run

1. Clone the repository  
   ```bash
   git clone https://github.com/yourusername/brats-segmentation-cvae.git
   cd brats-segmentation-cvae
    ```
2. Install dependencies

   ```bash
   pip install -r requirements.txt
   ```

3. **Download and preprocess dataset**

   * Download BraTS 2020 NIfTI files
   * Preprocess to normalize, crop/pad, and stack modalities

4. **Run the notebook**
   Launch `brats20-3dunet-3dautoencoder.ipynb` to train and evaluate models.

---

## 📊 Results

* ✅ 3D U-Net achieved high Dice coefficients on validation set.
* 🧪 CVAE produced realistic MRI volumes conditioned on tumor class.
* 🧠 Synthetic data improved model generalization in limited-data settings.

---

## 📌 Future Enhancements

* [ ] Integrate GAN-based data generation
* [ ] Deploy using FastAPI + Streamlit for real-time demo
* [ ] Evaluate on BraTS 2021/2023 datasets


---

## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

