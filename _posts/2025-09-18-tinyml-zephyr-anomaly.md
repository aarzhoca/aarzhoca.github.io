---
layout: post
title: "Deterministic TinyML on Zephyr: DMA, ISR, and Cache Pitfalls"
---

Objective: anomaly detection on an MCU **without** blowing real-time budgets.

**Key lessons**
- Use DMA-backed ring buffers; keep ISR handlers lean
- Pin memory regions for model buffers; mind cache coherency on M7/MPU targets
- Measure *worst-case* inference time (P95/P99) and enforce with a watchdog

Artifacts:
- Latency histograms in CI
- Fixed-point model configs
- Failing tests for boundary conditions (sensor silence, burst traffic)
