---
title: Debugging OpenVLA on LIBERO — From 0% to 99% Success
date: 2026-08-27
tags:
  - Vision-Language-Action
  - OpenVLA
  - LIBERO
  - Robot Manipulation
  - Imitation Learning
  - PyTorch
  - LoRA
categories:
  - Learning for Robotics
summary: A systematic integration study of OpenVLA and OpenVLA-OFT on the LIBERO manipulation benchmark, isolating eight bugs that silently drove success from 0% to 51.6% (base) and 99.2% (OFT) across 500 evaluation episodes.
featured: true
url_code: 'https://github.com/juttu-s/vla-libero-bench'
image:
  filename: featured.png
  preview_only: true
---

A **vision-language-action (VLA)** model that "loads successfully" and a VLA model that *works* are two very different things. This project benchmarks **OpenVLA** and **OpenVLA-OFT** on the **LIBERO** manipulation benchmark, and documents the gap between those two states.

The headline result is not the final accuracy — it is that a naive but seemingly correct integration scored **0% across 250 episodes**, and every point of recovery came from a specific, identifiable bug at the model–simulator boundary.

> **Code:** [github.com/juttu-s/vla-libero-bench](https://github.com/juttu-s/vla-libero-bench)

---

## Results

Each configuration was evaluated over **250 episodes**, with 95% Wilson confidence intervals.

### LIBERO-Spatial

| Configuration | Success Rate | 95% CI |
|---|---|---|
| Base OpenVLA — naive integration | **0.0%** | — |
| Base OpenVLA — after bug fixes | **51.6%** (129/250) | 45.4 – 57.7% |
| OpenVLA-OFT | **99.2%** (248/250) | 97.1 – 99.8% |

### LIBERO-Object

| Configuration | Success Rate | 95% CI |
|---|---|---|
| Base model, zero-shot | **0.0%** | — |
| Custom LoRA fine-tune | collapsed | — |
| Official fine-tuned checkpoint | **88.8%** (222/250) | 84.3 – 92.1% |

The official checkpoint result reproduces the published figure, which validates the harness itself — a necessary control before trusting any of the other numbers.

---

## The Eight Bugs

Each of these produced either silent failure or plausible-but-wrong behaviour. None raised an exception.

1. **Attention mask mismatch** in `transformers` — the installed attention backend disagreed with the mask layout the checkpoint expected. Resolved by pinning the **SDPA** implementation.
2. **Image orientation** — frames required a **180° rotation**, not the vertical flip that the obvious reading of the simulator convention suggests. A vertical flip produces images that look approximately right, which is exactly why it survives inspection.
3. **Inverted gripper convention** — the sign of the gripper channel is opposite between the training data and the simulation environment, so the policy opened when it intended to close.
4. **Center-crop semantics** — the documented 90% crop is **90% of *area***, not 90% per side. Getting this wrong shifts the effective field of view enough to break spatial grounding.
5. **Gripper command duration** — single-step gripper commands are insufficient; the actuator needs **temporal persistence with hysteresis** to actually complete a grasp.
6. **Dataset statistics merging** — normalization statistics from fine-tuning were only partially merged into the checkpoint, so actions were de-normalized against the wrong distribution.
7. **LIBERO package mapping** — a missing `__init__` file caused the installed package to expose empty module mappings, silently resolving task suites to nothing.
8. **Headless reset hang** — exception handling inside environment reset deadlocked under headless OpenGL rendering rather than surfacing an error.

---

## Method

- **Models:** OpenVLA (7B, base and LoRA-fine-tuned) and OpenVLA-OFT
- **Benchmark:** LIBERO-Spatial and LIBERO-Object, 250 episodes per configuration
- **Simulator:** MuJoCo with configurable OpenGL / EGL rendering backends
- **Diagnostics:** Per-bug isolation scripts under `scripts/`, with debug frame captures in `assets/` to visually confirm preprocessing at each stage
- **Reproducibility:** Pinned Conda environments under `env/`, results as raw episode records under `results/`

## Working Under a Single-GPU Budget

The whole study ran on **one 24 GB GPU**, which shaped the design:

- LoRA fine-tuning at **batch size 2 with 8× gradient accumulation** to fit in memory
- **SDPA** attention instead of flash-attention, since no CUDA toolkit was available to build it
- The custom LoRA run **collapsed** — reported rather than hidden, because it marks the real boundary of what this hardware budget supports

---

## Takeaway

The 51.6% → 99.2% jump from OpenVLA to OpenVLA-OFT is a genuine architectural result. The 0% → 51.6% jump is not a result at all — it is the cost of integration, and it is invisible in every paper that reports only the final number. Publishing the bug list is the useful contribution here.
