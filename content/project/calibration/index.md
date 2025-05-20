---
title: Camera Calibration and Augmented Reality
date: 2024-03-18
tags:
  - Camera Calibration
  - OpenCV
  - Augmented Reality
  - Pose Estimation
  - Virtual Projection
summary: Calibrated a camera using chessboard targets, estimated pose with solvePnP, and rendered real-time virtual objects onto scenes using OpenCV.
featured: true
image:
  filename: augmented_reality.png  # Save a screenshot to static/img/
  preview_only: true
---

This project focused on calibrating a camera and using it to overlay **virtual 3D objects in real-time video feeds** using OpenCV. It introduced concepts in camera intrinsics, pose estimation, and interactive augmented reality applications.

---

### 📌 Project Highlights

1. **Corner Detection & Calibration**  
   - Detected checkerboard corners using OpenCV  
   - Saved 3D-2D point correspondences  
   - Performed calibration with `cv2.calibrateCamera()`  
   - Achieved reprojection error ≈ 0.544

2. **Pose Estimation & Projection**  
   - Used `solvePnP()` to compute pose  
   - Visualized 3D axes on the image using `projectPoints`

3. **Render Virtual Objects**  
   - Designed a 15-point "C" shape object in world space  
   - Rendered its projection on camera view  
   - Preserved 3D orientation as the camera moved

---

### 🧠 Extra Features

- Harris corner detection to compare feature robustness  
- Live insertion of objects via webcam  
- Support for **multiple checkerboards** in one scene  
- Replaced the checkerboard region with a **custom image overlay**

---

### 🔍 Extension Tasks

- Compared calibrations of internal vs external webcams  
- Added keyboard control to insert virtual objects from pre-recorded videos  
- Used different board sizes (9x6, 6x6) in the same frame  
- Created **multi-object AR scenes** from multiple markers

---

### 📁 Resources

- 📄 [Project Report (PDF)](/files/Project%204-Report.pdf)
- 🎥 [Demo Video](https://drive.google.com/file/d/103mUiSgL6q1pJ2LhHZq8z1r2gVORhIdA/view?usp=sharing)
- 🔗 [GitHub Repository](https://github.com/juttu-s/augmented-reality-calibration)

---

This project was an exciting blend of **computer vision theory and practical AR rendering** using OpenCV. It forms a solid foundation for advanced applications in robotics, pose tracking, and mixed-reality interfaces.
