---
title: Semantic Geometric SLAM (SG-SLAM) in Dynamic Scenes
date: 2025-03-15
tags:
  - SLAM
  - Semantic SLAM
  - ORB-SLAM2
  - YOLO
  - Dynamic Environments
  - ROS
  - PyTorch
  - C++
summary: Integrated a YOLO-based object detector into the ORB-SLAM2 frontend to filter dynamic features, improving tracking accuracy by 31% on the TUM RGB-D dynamic sequences.
featured: true
image:
  filename: featured.png
  preview_only: true
---

This project implements **SG-SLAM (Semantic Geometric SLAM)**, a system that fuses **semantic object detection** with the geometric tracking pipeline of **ORB-SLAM2** to remain robust in **dynamic environments**. Standard feature-based SLAM systems assume a static world, so moving objects (e.g., walking people) corrupt the map and degrade pose estimation. SG-SLAM removes these dynamic features before they ever reach the optimizer.

---

## Motivation

Classical visual SLAM extracts and tracks features across frames under a **static-scene assumption**. When people or vehicles move through the scene, their features inject incorrect correspondences into the tracking thread, biasing pose estimates and polluting the global map. SG-SLAM addresses this by adding a **semantic layer** that identifies and rejects dynamic content.

---

## Approach

- **Semantic frontend:** Integrated a **YOLO-based object detection network** into the **ORB-SLAM2** tracking thread to detect a priori dynamic classes (e.g., humans).
- **Dynamic feature filtering:** Features falling inside detected dynamic bounding boxes are discarded before pose estimation and map optimization, preventing them from corrupting the map.
- **Geometric backend:** The remaining static features feed the standard ORB-SLAM2 tracking, local mapping, and loop-closure modules for consistent map optimization.
- **Stack:** Implemented in **C++** within ORB-SLAM2, with the detection network in **PyTorch**, integrated under **ROS**.

---

## Results

- Achieved a **31% accuracy improvement** on the **TUM RGB-D dynamic sequence** benchmarks.
- Prevented dynamic objects from corrupting the map optimization, yielding cleaner reconstructions and more stable trajectories in scenes with moving people.

---

## Tools & Libraries

- ORB-SLAM2 (C++)
- YOLO object detection (PyTorch)
- ROS
- TUM RGB-D Dataset (dynamic sequences)

---

This project demonstrates how a lightweight semantic layer can make geometric SLAM robust to real-world dynamics — a key requirement for deploying autonomous robots in environments shared with people.
