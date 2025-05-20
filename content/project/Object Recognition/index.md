---
title: Real-Time 2D Object Recognition with Feature Matching
date: 2024-03-30
tags:
  - Object Recognition
  - OpenCV
  - Feature Extraction
  - Real-Time Systems
  - Computer Vision
summary: Built a webcam-based 2D object recognition system using shape descriptors, feature vectors, and both Euclidean and KNN-based classification strategies.
featured: true
image:
  filename: object_recognition.png  # Place a screenshot in static/img/
  preview_only: true
---

This project developed a **real-time webcam-based system** to detect and classify 2D objects using image segmentation, shape features, and distance-based classifiers. The system supports capturing and labeling training data interactively and recognizes both scale- and rotation-invariant objects.

---

### 🧠 Workflow

1. **Thresholding Input Frames**  
   - Dynamic thresholding via simplified K-means clustering  
   - Binary image separates object from background

2. **Morphological Filtering**  
   - Used dilation and erosion to clean noise and fill holes

3. **Connected Components & Region Segmentation**  
   - Identified distinct objects  
   - Filtered out small noisy components

4. **Feature Extraction**  
   - Centroids, central moments, bounding box, percent fill  
   - Orientation angle from least central moment

5. **Training Interface**  
   - Press `'n'` to label new objects and save features to CSV

6. **Classification (2 Methods)**  
   - **Baseline:** Scaled Euclidean distance  
   - **KNN (k=4):** Chosen label from majority of 4 nearest neighbors

7. **Confusion Matrix Evaluation**  
   - Achieved 93–100% accuracy on 5 classes  
   - Evaluated with multiple images per class under varied conditions

---

### 🔧 Extended Features

- Recognizes **11 total object classes**  
- Handles **multiple objects** simultaneously in a frame  
- Classifies objects even under **rotations and scaling**

---

### 🔁 Demo Mode

- Press `'r'` to begin recording video  
- Press `'p'` to stop and save to MP4

🎥 [Live System Demo](https://drive.google.com/file/d/1AFoqLXxugcIa1uGtxgGTe1So_fgyTtBC/view?usp=sharing)

---

### 📁 Resources

- 📄 [Project Report (PDF)](/files/Project%203-Report.pdf)
- 🔗 [GitHub Repository](https://github.com/juttu-s/real-time-object-classifier)

---

This project combines classic computer vision with real-time systems and demonstrates how simple shape-based features can provide surprisingly effective results when paired with robust classification logic.
