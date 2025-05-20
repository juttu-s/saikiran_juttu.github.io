---
title: Kimera VIO on EuRoC and Custom Datasets
date: 2024-04-26
tags:
  - Visual-Inertial Odometry
  - Kimera
  - SLAM
  - GTSAM
  - Pose Estimation
summary: Implemented Kimera VIO on both EuRoC MAV and a custom dataset to evaluate trajectory accuracy, runtime performance, and robustness under varying visual-inertial conditions.
featured: true
image:
  filename: kimera_traj.png  # Save any Kimera trajectory image to static/img/
  preview_only: true
---

This project evaluates the **Kimera Visual-Inertial Odometry (VIO)** framework on two datasets — the **EuRoC MAV benchmark** and a **custom indoor dataset** — to assess its accuracy, runtime efficiency, and adaptability.

---

### 🧠 Project Goals

- Set up Kimera VIO in a ROS + Docker environment  
- Run it on benchmark and custom datasets  
- Evaluate using ATE RMSE, runtime, and qualitative analysis

---

### 🔍 Methodology

**VIO Front-End:**
- Feature detection (Shi-Tomasi)
- Optical flow tracking (Lucas-Kanade)
- Depth estimation via stereo matching
- Outlier filtering for robust constraints

**VIO Back-End:**
- Factor graph construction (GTSAM)
- iSAM2 for incremental optimization
- Pose, velocity, and landmark estimation

---

### 🧪 Evaluation

#### ✅ Dataset 1: EuRoC MAV
- Ran Kimera VIO on V1_01 to V1_03
- Compared RMSE with VINS-Mono, OKVIS, MSCKF
- Achieved best accuracy across all sequences
- Average RMSE: 0.05–0.08

#### 🧪 Dataset 2: Custom D455 Dataset
- Real-world indoor environment
- Feature-sparse and dynamically lit scenes
- Maintained smooth and consistent trajectory
- Minor drift in Z axis corrected by loop closures

---

### ⚙️ Tools & Libraries

- **Kimera VIO** from MIT-SPARK Lab
- **GTSAM** for factor graph optimization
- **Open3D**, **Matplotlib** for visualization
- **Intel Realsense D455**, ROS, Docker

---

### 🧾 Resources

- 📄 [Project Report (PDF)](/files/MR_Project_Report.pdf)
- 🔗 [Kimera VIO GitHub](https://github.com/MIT-SPARK/Kimera-VIO)

---

Kimera VIO proved to be a robust, modular SLAM framework capable of producing accurate trajectories under both structured (EuRoC) and challenging (custom indoor) conditions. Loop closure and factor graph smoothing allowed it to adapt well even with limited visual features.
