# Cardiac Arrhythmia Prediction using Dual-Scale 1D CNN

<p align="left">
  <img src="https://img.shields.io/badge/Python-3.8+-blue.svg" alt="Python Version">
  <img src="https://img.shields.io/badge/PyTorch-Deep%20Learning-ee4c2c.svg" alt="PyTorch">
  <img src="https://img.shields.io/badge/Dataset-MIT--BIH-success.svg" alt="Dataset">
  <img src="https://img.shields.io/badge/Evaluation-LOSO-orange.svg" alt="LOSO Protocol">
</p>

## 📌 Project Overview
This repository contains a robust deep learning pipeline for predicting cardiac arrhythmias from Electrocardiogram (ECG) signals. The project focuses on a **Dual-Scale 1D Convolutional Neural Network (CNN)** designed to capture both fine morphological beat features (intra-beat) and broader rhythm dynamics (inter-beat).

To ensure clinical relevance and prevent data leakage, the models are evaluated under a strict, patient-independent **Leave-One-Subject-Out (LOSO)** cross-validation protocol.

## 📊 Dataset
The models are trained and evaluated on the widely recognized **MIT-BIH Arrhythmia Database**. 
* The original annotations are mapped to the standard **AAMI 5-class system**:
  * **N:** Normal sinus rhythm
  * **S:** Supraventricular ectopic beat
  * **V:** Ventricular ectopic beat
  * **F:** Fusion beat
  * **Q:** Unknown beat
* Data from identical patients (e.g., records 201 and 202) are merged into single test subjects during LOSO folds to guarantee zero patient overlap between training and testing sets.

## 🧠 Methodology & Architecture
* **Intra-Beat Scale:** A dual-branch 1D CNN encoder extracting morphological features from 2-lead, 300-sample single heartbeats.
* **Inter-Beat Scale:** A sequential 1D CNN encoder processing a 9-beat sequence (the focal beat + 8 surrounding context beats) to capture temporal rhythm patterns.
* **Optimization:** Trained using **Focal Loss** ($\gamma = 2.0$) with inverse-frequency class weighting to address the severe class imbalance inherent in clinical ECG data, optimized via AdamW and OneCycleLR scheduling.

## 🚀 Key Results
The Dual-Scale 1D CNN achieved the following aggregate performance under the LOSO protocol:

* **Overall Accuracy:** 88.44%
* **Macro-Average F1-score:** 0.5787

| Class | Precision | Recall | F1-Score | Support |
| :--- | :--- | :--- | :--- | :--- |
| **N** (Normal) | 0.96 | 0.91 | 0.93 | 90,588 |
| **S** (Supraventricular)| 0.13 | 0.24 | 0.17 | 2,781 |
| **V** (Ventricular) | 0.77 | 0.87 | 0.82 | 7,235 |
| **F** (Fusion) | 0.08 | 0.15 | 0.11 | 802 |
| **Q** (Unknown) | 0.85 | 0.88 | 0.87 | 8,038 |

## ⚙️ Installation & Usage

1. **Clone the repository:**
   ```bash
   git clone https://github.com/sr-hridoy/cardiac-arrhythmia-prediction.git
   cd cardiac-arrhythmia-prediction
   ```

2. **Install dependencies:**
   Ensure you have Python 3.8+ installed. Install the required packages using:
   ```bash
   pip install -r requirements.txt
   ```

## 👨‍💻 Author
**Md. Shaifur Rahman Hridoy**  
*B.Sc. in Computer Science and Engineering, Leading University*  

Feel free to reach out or open an issue if you have questions about the implementation or research methodology!
