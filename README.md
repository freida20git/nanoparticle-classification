# Nanoparticle Classification with SAM vs YOLO

## Project Goal

This project compares the performance of **Segment Anything Model (SAM)** and **YOLOv11** for classifying different nanoparticle shapes (triangles, dots, and cubes).  
We show that **SAM-based pipelines** significantly outperform YOLO—even with small datasets.

All data used in this project can be accessed here: [Google Drive Link](_____link_____)

---

## Paper: 

[Zero-shot Shape Classification of Nanoparticles in SEM Images using Vision Foundation Models](https://arxiv.org/abs/2508.03235) 

---
## Performance Summary
results could be found in `Summary_Table.pdf` file.
---

## 📁 Repository Structure Description

- **triangles/**  
  Contains all scripts related to triangle-shaped nanoparticles.  
  Includes:
  - SAM segmentation and mask extraction
  - DINOv2-based feature extraction and classification (validation and test)
  - YOLOv11 training notebook for triangle data

- **cubes/**  
  Contains all scripts related to cube-shaped nanoparticles.  
  Includes:
  - SAM segmentation and mask extraction
  - DINOv2-based feature extraction and classification (validation and test)
  - YOLOv11 training notebook for cube data

- **dots/**  
  Contains all scripts related to dot-like nanoparticle classification.  
  Includes:
  - SAM segmentation and mask extraction
  - DINOv2-based feature extraction and classification (validation and test)
  - YOLOv11 training notebook for dot data

- **results/**  
  Contains output tables, performance metrics, and summary comparisons (e.g., Recall, Precision, F1-scores of SAM vs YOLO).

---
## File Descriptions

### 🔺 Triangles

- `cut_triangles_sam.ipynb`  
   Generates segmentation masks using the **SAM** model and saves cropped triangle regions.

- `triangles_silhouette_validation_dinov2.ipynb`  
   Extracts embeddings with DINOv2 for training and evaluating classifiers (SVM, RF, LR, NB) using silhouette & separation scores.

- `triangles_silhouette_test_dinov2.ipynb`  
   Evaluates model generalization on unseen triangle data. Includes PCA, confusion matrix, classification report.

- `yolo_training_triangles.ipynb`  
   Trains a **YOLO** model for detecting triangle subtypes. Includes data prep and model evaluation.

### 🧊 Cubes

- Same structure as the `triangles/` folder, using cube images instead.
  - `cut_cubes_sam.ipynb`  
  - `cubes_silhouette_validation_dinov2.ipynb`  
  - `cubes_silhouette_test_dinov2.ipynb`  
  - `yolo_training_cubes.ipynb`

### ⚪ Dots

- Same structure as the `triangles/` folder, using dot images instead.
  - `cut_dots_sam.ipynb`  
  - `dots_silhouette_validation_dinov2.ipynb`  
  - `dots_silhouette_test_dinov2.ipynb`  
  - `yolo_training_dots.ipynb`
 
---
## Data Availability

The full dataset is available at:  
[Nanoparticle Classification Data (Google Drive)](https://drive.google.com/drive/folders/1GdorkrrcLbj-b55gbeYYuipEBSp8yCJm)

The data is organized into three main folders:
- **Triangles/**
- **Dots/**
- **Cubes/**

Each of these folders includes:



### 1. Full Images Folder

Contains original microscopy images, categorized into:
- `train/` — for training
- `valid/` — for validation
- `test/` — for final testing

Each image filename indicates the type and index, e.g., `triangle_train2.jpg`.


### 2. Masked Segmentations Folder

Contains cropped single-particle images (as `.jpg`) extracted using the SAM model.  
They are organized into class-specific subfolders, such as:
- `triangle/`, `circle/`, `truncated/` (inside the `Triangles/` folder)

Each filename is formatted as:

datasetName_imageName_x1_y1_x2_y2.jpg

Where:
- `x1`, `y1` = bottom-left corner of bounding box  
- `x2`, `y2` = top-right corner of bounding box

#### Example:

triangles/truncated/triangle_train2_234_105_554_667.jpg

This means:
- The object was extracted from `triangle_train2.jpg`
- It was classified as a **truncated triangle**
- The bounding box in the original image spans from `(234, 105)` to `(554, 667)`


### YOLO Annotation labels

For YOLOv11 training, bounding box annotations were automatically converted to YOLO format using code in the training notebooks.

Each image has a corresponding `.txt` file:

yolo_labels/image_name.txt

Each line in a label file follows the YOLO annotation format:

class_id x_center_norm y_center_norm width_norm height_norm

Where:
- All values are **normalized** by the image width and height  
- Each object in the image is represented by one line

YOLO label files are available here:   [YOLO Labels (Google Drive)](link) 


---

