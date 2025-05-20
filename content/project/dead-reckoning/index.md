---
title: Dead Reckoning with IMU & GPS in Vehicle Navigation
date: 2024-03-15
tags:
  - IMU
  - GPS
  - Dead Reckoning
  - Sensor Fusion
  - ROS
  - Navigation
summary: Fused IMU and GPS data to perform dead reckoning in a high-speed vehicle and evaluated accuracy through heading estimation, velocity integration, and trajectory reconstruction.
featured: true
image:
  filename: imu_vs_gps.png  # Add trajectory comparison image to static/img/
  preview_only: true
---

This project involved real-world testing of **dead reckoning navigation** using an **IMU (VectorNav 100)** and GPS data mounted in a car. We collected and fused sensor data to estimate vehicle trajectory and compared it against ground truth GPS tracks.

---

### 📍 Objective

- Use IMU (accel, gyro, mag) for estimating yaw and velocity
- Compare integrated dead reckoning trajectory with GPS
- Apply calibration and filtering for high-speed vehicle navigation

---

### 🧪 Methodology

1. **Sensor Mounting & Data Collection**  
   - IMU mounted flat, aligned to vehicle axis  
   - GPS puck on roof  
   - ROS bagged data over a 2–3 km drive around Boston

2. **Magnetometer Calibration**  
   - Applied hard & soft iron corrections using ellipse fitting  
   - Centered & scaled magnetometer output

3. **Yaw Estimation**  
   - Used complementary filter combining:
     - Low-pass filtered magnetometer (0.5 Hz cutoff)
     - High-pass filtered gyro data (0.1 Hz cutoff)
   - Fusion coefficient α = 0.98

4. **Velocity Estimation**  
   - Acceleration filtered with high-pass Butterworth  
   - Integrated over time  
   - Clamped negative values to zero and capped outliers

5. **Trajectory Reconstruction**  
   - Integrated filtered heading + velocity  
   - Rotated & scaled to align IMU trajectory with GPS path  
   - Best match scale: 2.25, rotation correction: 14–25°

---

### 📊 Results

- Initial path tracking was highly accurate  
- IMU-based dead reckoning remained within **2m** of GPS for **150–200 seconds**
- Final drift reached nearly **400 meters** after extended driving
- GPS helps correct IMU drift over long durations

---

### 🔎 Key Insights

- IMU is accurate for short-term dead reckoning  
- Drift arises from gyroscope bias and sloped paths  
- Regular GPS re-calibration is essential for long-term navigation  
- Complementary filter effectively combines noisy sensors

---

### 📁 Resources

- 📄 [Lab 5 Report (PDF)](/files/LAB%205%20report-1.pdf)
- 🔗 [GitHub Repository](https://github.com/juttu-s/dead-reckoning-imu-gps)

---

This project demonstrates real-world dead reckoning with consumer-grade sensors and sets the foundation for more robust SLAM and localization strategies in mobile robotics or autonomous vehicles.
