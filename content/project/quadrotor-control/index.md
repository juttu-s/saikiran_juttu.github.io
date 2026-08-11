---
title: Control Strategies for Quadrotor Position and Altitude
date: 2024-12-10
tags:
  - Control Systems
  - Quadrotor
  - MPC
  - LQR
  - LQG
  - MATLAB
  - Simulink
summary: A comparative study of MPC, LQR, LQG, and LQR-PI controllers for quadrotor position and altitude control, evaluating stability and robustness under sensor noise and disturbances.
featured: true
image:
  filename: featured.png
  preview_only: true
---

This project presents a **comprehensive comparative study of optimal control strategies** for **quadrotor position and altitude control**. The goal was to evaluate how different controllers handle stability, tracking accuracy, and robustness when subjected to realistic flight conditions such as **sensor noise** and **process disturbances**.

---

## Objectives

- Model the quadrotor dynamics and design controllers for position and altitude regulation.
- Implement and compare multiple optimal-control formulations on the same plant.
- Assess stability, adaptability, and robustness under real-world disturbances.

---

## Controllers Implemented

- **Model Predictive Control (MPC)** — constraint-aware optimization over a receding horizon.
- **Linear Quadratic Regulator (LQR)** — optimal state-feedback gain minimizing a quadratic cost.
- **Linear Quadratic Gaussian (LQG)** — LQR combined with a Kalman estimator for noisy state feedback.
- **LQR-PI** — LQR augmented with integral action to eliminate steady-state error.

---

## Evaluation

- Each controller was tested in **MATLAB / Simulink** on the quadrotor model.
- Performance was evaluated on **stability** and **adaptability**, explicitly incorporating real-world factors such as **sensor noise** and **process disturbances** to ensure robust flight dynamics.
- Compared tracking response, settling behavior, and disturbance rejection across the controllers.

---

## Tools & Libraries

- MATLAB
- Simulink
- Control System Toolbox

---

This study highlights the trade-offs between predictive, state-feedback, and estimator-based control for aerial robotics — informing controller selection for robust quadrotor flight in noisy, disturbance-prone environments.
