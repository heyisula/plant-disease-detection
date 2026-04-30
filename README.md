# 🌿 Pepper Bell Leaf Disease Detection
### Image Processing — Individual Project | HNDCSAIS25.2

A computer vision pipeline that detects **Bacterial Spot disease** in pepper bell leaves using HSV colour segmentation, GLCM texture analysis, and an SVM classifier — achieving automated disease diagnosis without any deep learning framework.

---

## 📁 Project Structure

```
project/
│
├── data/
│   ├── healthy/                  # Pepper__bell___healthy (100 sampled)
│   └── diseased/                 # Pepper__bell___Bacterial_spot (100 sampled)
│
├── plant_disease_detection.ipynb # Main notebook
├── README.md
│
└── out/
    ├── output_samples.png
    ├── output_preprocessing.png
    ├── output_segmentation.png
    ├── output_contours.png
    ├── output_edge_detection.png
    ├── output_confusion_matrix.png
    ├── output_disease_distribution.png
    └── output_predictions.png
```

---

## 📌 Problem Statement

Bacterial spot is one of the most damaging diseases affecting pepper crops, causing significant yield loss if not identified early. Traditional diagnosis relies on manual inspection by agricultural experts — a process that is slow, expensive, and difficult to scale. This project automates the detection process using image processing, making it accessible without specialised equipment.

---

## 🗃️ Dataset

**Source:** [PlantVillage Dataset — Kaggle](https://www.kaggle.com/datasets/emmarex/plantdisease)

| Class | Folder | Total Available | Used |
|---|---|---|---|
| Healthy | `Pepper__bell___healthy` | 1,478 | 100 |
| Diseased | `Pepper__bell___Bacterial_spot` | 997 | 100 |
| **Total** | | **2,475** | **200** |

Images are randomly sampled with a fixed seed (`random.seed(42)`) to ensure reproducibility.

---

## ⚙️ Pipeline Overview

```
Raw Leaf Image
      │
      ▼
 1. Preprocessing          Resize to 128×128 · Gaussian Blur (noise removal)
      │
      ▼
 2. Colour Segmentation    HSV masking → isolate green (healthy) and brown/yellow (disease) regions
      │
      ▼
 3. Contour Detection      findContours → count and measure individual disease spots
      │
      ▼
 4. Edge Detection         Canny edge detection → visualise spot boundaries
      │
      ▼
 5. Feature Extraction     Colour histogram (HSV) + GLCM texture + spot statistics
      │
      ▼
 6. Classification         StandardScaler → SVM (RBF kernel) → Prediction
      │
      ▼
 7. Evaluation             Accuracy · Precision · Recall · F1 · Confusion Matrix
```

---

## 🔬 Techniques Used

| Technique | Purpose |
|---|---|
| Gaussian Blur | Noise reduction before segmentation |
| HSV Colour Masking | Separate healthy green tissue from diseased brown/yellow spots |
| Morphological Operations | Clean up segmentation mask (open + dilate) |
| Canny Edge Detection | Highlight boundaries of disease lesions |
| `cv2.findContours` | Count and measure individual disease spots |
| HSV Colour Histogram | Capture colour distribution per image (48 features) |
| GLCM (Grey-Level Co-occurrence Matrix) | Capture surface texture — contrast, homogeneity, energy, correlation |
| SVM with RBF Kernel | Binary classification: healthy vs bacterial spot |
| StandardScaler | Normalise features before feeding into SVM |

---

## 📦 Requirements

```
Python 3.8+
opencv-python
scikit-image
scikit-learn
matplotlib
seaborn
numpy
```

Install all dependencies:

```bash
pip install opencv-python scikit-image scikit-learn matplotlib seaborn numpy
```

---

## 🚀 How to Run

1. Clone or download this repository
2. Place your dataset images into the correct folders:
   ```
   images/healthy/    ← images from Pepper__bell___healthy
   images/diseased/   ← images from Pepper__bell___Bacterial_spot
   ```
3. Open the notebook:
   ```bash
   jupyter notebook plant_disease_detection.ipynb
   ```
4. Run all cells top to bottom (`Kernel → Restart & Run All`)
5. Output images will be saved automatically in the same directory

---

## 📊 Results

All result visualisations are saved as `.png` files during execution:

| Output File | Description |
|---|---|
| `output_samples.png` | Sample images from both classes |
| `output_preprocessing.png` | Before and after Gaussian blur |
| `output_segmentation.png` | HSV segmentation masks and disease overlays |
| `output_contours.png` | Detected disease spot contours |
| `output_edge_detection.png` | Canny edge detection result |
| `output_disease_distribution.png` | Histogram of disease area % per class |
| `output_confusion_matrix.png` | SVM classifier confusion matrix |
| `output_predictions.png` | Sample predictions on test images |

---

## 📝 Notes

- Feature vector per image: **56 features** (48 colour histogram + 5 GLCM texture + 3 spot statistics)
- Train/test split: **80% / 20%** with stratified sampling
- The model and scaler are fit only on training data to prevent data leakage
- All randomness is seeded for reproducibility

