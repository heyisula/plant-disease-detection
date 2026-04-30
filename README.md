<div align="center">

# 🌿 Plant Disease Detection
### Pepper Bell Leaf  Bacterial Spot Classification

<br/>

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-4.x-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.x-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)

<br/>

![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=flat-square)
![Dataset](https://img.shields.io/badge/Dataset-PlantVillage-blue?style=flat-square)
![Images](https://img.shields.io/badge/Images-200-orange?style=flat-square)
![Classifier](https://img.shields.io/badge/Classifier-SVM_RBF-9cf?style=flat-square)

<br/>

> Detecting bacterial spot disease in pepper bell leaves using classical image processing techniques combined with machine learning — designed as a low-cost alternative to expert visual inspection.

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Dataset](#-dataset)
- [Project Pipeline](#-project-pipeline)
- [Techniques Used](#-techniques-used)
- [Installation](#-installation)
- [Usage](#-usage)
- [Output Files](#-output-files)
- [Project Structure](#-project-structure)
- [Results](#-results)

---

## 🔍 Overview

Bacterial spot is one of the most common and damaging diseases affecting pepper plants worldwide. Early detection is critical to prevent crop loss. This project builds an image-processing pipeline that can automatically distinguish between **healthy** and **bacterially infected** pepper bell leaves using:

- **Color-based segmentation** in the HSV color space
- **Texture analysis** using Gray-Level Co-occurrence Matrix (GLCM)
- **Contour detection** to locate and count disease spots
- **SVM classification** trained on extracted visual features

---

## 📂 Dataset

This project uses the **PlantVillage Dataset** — specifically the pepper bell subset.

| Class | Folder | Count Used |
|---|---|---|
| Healthy | `Pepper__bell___healthy` | 100 |
| Diseased | `Pepper__bell___Bacterial_spot` | 100 |
| **Total** | | **200** |

> The full dataset is available on [Kaggle — PlantVillage](https://www.kaggle.com/datasets/emmarex/plantdisease).  
> Only 100 images per class are randomly sampled at runtime.

---

## 🔄 Project Pipeline

```
Raw Leaf Image
      │
      ▼
┌─────────────────────────┐
│   1. Preprocessing      │  Resize to 128×128, Gaussian Blur (noise reduction)
└──────────┬──────────────┘
           │
           ▼
┌─────────────────────────┐
│  2. HSV Segmentation    │  Isolate green (healthy) and brown/yellow (diseased) regions
└──────────┬──────────────┘
           │
           ▼
┌─────────────────────────┐
│  3. Contour Detection   │  Detect individual disease spots, count them
└──────────┬──────────────┘
           │
           ▼
┌─────────────────────────┐
│  4. Feature Extraction  │  Color histogram + GLCM texture + Spot features
└──────────┬──────────────┘
           │
           ▼
┌─────────────────────────┐
│  5. SVM Classifier      │  Trained on extracted features, RBF kernel
└──────────┬──────────────┘
           │
           ▼
    Classification Result
  (Healthy / Bacterial Spot)
```

---

## 🛠 Techniques Used

| Technique | Purpose |
|---|---|
| Gaussian Blur | Noise removal before segmentation |
| HSV Color Space | Separate disease spots from healthy green tissue |
| Morphological Operations | Clean up segmentation masks (open + dilate) |
| Canny Edge Detection | Highlight boundaries of disease regions |
| `findContours` | Detect and count individual lesions |
| GLCM (Gray-Level Co-occurrence Matrix) | Capture texture differences between classes |
| Color Histogram (HSV) | Encode color distribution as features |
| SVM with RBF Kernel | Binary classification on extracted feature vectors |
| StandardScaler | Normalize features before feeding to SVM |

---

## ⚙️ Installation

**1. Clone or download this repository**

```bash
git clone https://github.com/heyisula/plant-disease-detection.git
cd plant-disease-detection
```

**2. Install dependencies**

```bash
pip install opencv-python scikit-image scikit-learn seaborn matplotlib numpy
```

Or install from the requirements file:

```bash
pip install -r requirements.txt
```

**`requirements.txt`**

```
opencv-python
scikit-image
scikit-learn
seaborn
matplotlib
numpy
```

---

## 🚀 Usage

**1. Organize your dataset**

```
project/
├── data/
│   ├── healthy/        ← paste images from Pepper__bell___healthy here
│   └── diseased/       ← paste images from Pepper__bell___Bacterial_spot here
├── train.ipynb
└── README.md
```

**2. Open the notebook**

```bash
jupyter notebook plant_disease_detection.ipynb
```

**3. Update the paths in Cell 2 if needed**

```python
healthy_folder  = 'data/healthy'
diseased_folder = 'data/diseased'
```

**4. Run All Cells**

`Kernel → Restart & Run All`

All output images are saved automatically to the project folder.

---

## 📤 Output Files

| File | Description |
|---|---|
| `output_samples.png` | Sample images from both classes |
| `output_preprocessing.png` | Before vs after Gaussian blur |
| `output_segmentation.png` | HSV masks and disease overlay |
| `output_contours.png` | Detected disease spot contours |
| `output_edge_detection.png` | Canny edge detection result |
| `output_disease_distribution.png` | Disease % histogram per class |
| `output_confusion_matrix.png` | SVM classifier confusion matrix |
| `output_predictions.png` | Sample predictions on test images |

---

## 🗂 Project Structure

```
plant-disease-detection/
│
├── data/
│   ├── healthy/
│   └── diseased/
│
├── out/                ← outputs
│
├── docs/               ← project documentation
│
├── train.ipynb         ← main notebook
├── requirements.txt
└── README.md
```

---

## 📊 Results

- **Feature Vector Size:** 56 features per image (48 color + 5 texture + 3 spot features)
- **Train / Test Split:** 80% / 20% (stratified)
- **Classifier:** SVM with RBF kernel (`C=10`, `gamma='scale'`)
- **Key Observation:** Diseased leaves showed significantly higher brown/yellow pixel ratios and greater GLCM contrast values compared to healthy leaves, making them reliably separable using extracted features alone.

<div>
