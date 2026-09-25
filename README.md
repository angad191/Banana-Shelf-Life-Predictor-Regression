# 🍌 Banana Ripeness Predictor: A Computer Vision Approach to Shelf-Life Estimation

![Python](https://img.shields.io/badge/Python-3.x-blue?style=flat-square&logo=python)
![OpenCV](https://img.shields.io/badge/Computer_Vision-OpenCV-green?style=flat-square&logo=opencv)
![Scikit-Learn](https://img.shields.io/badge/ML-Scikit--Learn-orange?style=flat-square&logo=scikit-learn)

> **Course:** Introduction to Machine Learning (IT3002) | **Institute:** IIIT-Allahabad

## 📖 Overview

Food waste is a critical global issue, with significant losses occurring in the logistics chain. [cite_start]Traditional fruit ripeness detection often relies on simple classification (e.g., "Ripe" vs. "Rotten"), which fails to provide the granular data needed for dynamic supply chain management.

This project introduces a **Time-Series Regression Framework** to predict the exact **remaining shelf-life (in days)** of bananas. Unlike simple single-feature models, our approach utilizes a robust multi-feature vector derived from a custom dataset to handle the ambiguity between ripening and rotting visual signals.

---

## 🚀 Key Features

* **Regression vs. Classification:** Predicts a continuous value (e.g., "1.5 days left") rather than discrete categories, enabling precise inventory prioritization.
* **Novel Time-Series Dataset:** Built from scratch using 66 images of 7 distinct bananas tracked over 5 days under controlled environmental conditions.
* **Robust Feature Engineering:** Utilizes a statistically validated 4-feature vector that outperforms single-feature models like Mean Hue, which we proved to be ambiguous.
* **"Digital Cutout" Preprocessing:** Implements a manual background removal pipeline to eliminate shadow artifacts that confuse brown spot detection.

---

## 🔬 Methodology

### 1. Data Acquisition & Preprocessing
Images were captured daily using a Samsung Galaxy S23 (108MP) under ambient lighting. To eliminate environmental noise, we developed a "Digital Cutout" technique, isolating the banana on a pure white background (`#FFFFFF`) to ensure accurate feature extraction.

### 2. Feature Selection ("The Golden Set")
We analyzed 9 potential visual features using Pearson correlation ($r$) and Coefficient of Variation ($CV$). We selected 4 robust features that statistically correlate with ripening while resisting camera auto-exposure noise:

| Feature | Description | Correlation ($r$) | Role |
| :--- | :--- | :--- | :--- |
| **Hue Mean** | Average color tone | $0.72$ | Tracks yellowing trend. |
| **Saturation StdDev** | Color variance | $-0.66$ | Captures uneven ripening. |
| **Brown Percentage** | Area of decay spots | $-0.59$ | Direct measure of sugar spots/rot. |
| **Laplacian Variance** | Texture complexity | $0.31$ | Measures surface wrinkling. |

### 3. Model "Bake-Off"
We trained and evaluated 6 different regression models using **5-Fold Cross-Validation**.

| Model | Mean MAE (Days) | $R^2$ Score | Verdict |
| :--- | :--- | :--- | :--- |
| **Linear Regression** | **0.7015** | **0.6288** | 🏆 **Champion** |
| Support Vector (SVR) | 0.7700 | 0.6093 | Runner Up |
| k-Nearest Neighbors | 0.8095 | 0.5784 | - |
| Random Forest | 0.8309 | 0.5616 | Overfitting |
| Polynomial (Deg 3) | 2.1566 | -4.60 | Catastrophic Failure |

> **Insight:** The simple Linear Regression model outperformed complex non-linear models (like Random Forest), adhering to Occam's Razor for our small, high-quality dataset.

---

## 🛠️ Tech Stack

* **Language:** Python 3.x
* **Computer Vision:** OpenCV (`cv2`) for color space conversion (HSV), thresholding, and edge detection [Notebook Cell 3].
* **Machine Learning:** Scikit-Learn for regression models, pipelines, and cross-validation [Notebook Cell 2].
* **Data Manipulation:** Pandas & NumPy [Notebook Cell 2].
* **Environment:** Google Colab / Jupyter Notebook [Notebook Cell 1].

---

## 💻 Installation & Usage

### Prerequisites
Ensure you have the necessary Python libraries installed:

```bash
pip install opencv-python-headless pandas numpy scikit-learn openpyxl
```
### Running the Predictor
The project is contained within a single interactive Jupyter Notebook.

1. Clone the Repo (or download the notebook).

2. Open Banana_Ripeness_Notebook.ipynb.

3. Run Cells 1 & 2 to import libraries and define the feature extractor function [Notebook Cell 2, 3].

4. Run Cell 3 (Data Acquisition): Upload the provided dataset images to generate the feature matrix Excel file [Notebook Cell 4].

5. Run Cell 4 (Evaluation): See the cross-validation comparison of all models [Notebook Cell 5].

6. Run Cell 5 (App): The notebook will launch an interactive tool. Upload a new image of a banana (on a white background), and the model will predict how many days it has left [Notebook Cell 6]!
---

## 📊 Repository Structure
```plaintext
📂 Banana-Ripeness-Predictor
├── 📄 Banana_Ripeness_Notebook_Group41.ipynb  # Main Code
├── 📄 IML_Final_Project_Report.pdf            # Detailed Research Paper
├── 📂 dataset                                 # Folder containing the 66 raw images
├── 📄 banana_analysis_results.xlsx            # Generated feature dataset
└── 📄 README.md                               # Project Documentation
```
---

## 👥 Team Members (Group 41)

- Hargun Preet Singh (IIT2023191) - Methodology & Pipeline Design 

- Adarsh Kumar (IIT2023194) - Data Acquisition & Ground Truth 

- Rounak Dagar (IIT2023195) - Statistical Analysis & Feature Engineering 

- Kanishk Sakarwar (IIT2023210) - Validation & Reporting 
---

## 📄 License
This project is open-source and available under the MIT License.

> **Note on Replication**: For best results when testing the interactive app, ensure your input image has a clean white background, similar to the training data. This ensures the computer vision algorithms correctly isolate the fruit.
---
