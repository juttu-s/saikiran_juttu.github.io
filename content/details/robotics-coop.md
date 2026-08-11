---
title: "Robotics Engineer Co-op"
summary: "Integrated SLAM, embedded deployment, UAV motion planning, and semantic vision for autonomous robots."
date: 2025-05-01
tags: ["ROS2", "Jetson", "SLAM", "OptiTrack", "VLM", "Perception"]
image:
  filename: experience-banner.png
  preview_only: true
---

## Overview

Worked at Northeastern University on:

---

### Sensor Integration

Integrated **3D LiDAR and Intel RealSense** sensors with the **Scout Mini Rover** via CAN protocol in ROS 2, deployed on **Jetson AGX Orin** for synchronized perception, sensor fusion, and reliable HW–SW communication.

**Physical Setup**
![Scout Mini Rover Setup](/saikiran_juttu.github.io/uploads/Robot.jpeg)


### SLAM Implementation

Implemented ROS 2-based **SLAM systems** using:

- RTAB-Map
- LIO-SAM
- Visual-Inertial Odometry (VIO)
- SLAM Toolbox  
In C++/Python with Nav2 for improved localization in GPS-denied environments.

**RTAB-Map Demo:**

<video controls width="100%" muted autoplay loop>
  <source src="/saikiran_juttu.github.io/uploads/RTAB_demo.mp4" type="video/mp4">
</video>

**LIO-SAM Screenshot:**

![LIO-SAM Visualization](/saikiran_juttu.github.io/uploads/lio_sam.png)

---

### UAV Motion Planning

Developed **waypoint navigation and motion planning** pipelines for **Crazyflie and DJI Tello** using the **OptiTrack motion capture system**.

- Automated takeoff
- Precision landing
- Closed-loop control with state estimation

---

### Semantic Perception with VLMs

Exploring integration of **Vision-Language Models (VLMs)** to:

- Enhance indoor semantic navigation
- Reduce localization drift
- Enable autonomous scene understanding
