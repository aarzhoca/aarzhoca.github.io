---
layout: post
title: "VR Wrist EMG Interface & System Lab — Hobby Project"
description: "Reproducible EMG+IMU pipeline for VR/AR with a Rust host service, record→replay tools, and HIL-friendly metrics."
permalink: /posts/vr-wrist-emg-lab/
date: 2025-10-23
tags: [vr, emg, embedded, rust, systems, hil]
image: /assets/emg-lab/cover.png
---

I’ve been exploring wrist EMG as an input path for VR/AR. This post shares a small, reproducible pipeline:

**EMG AFE → MCU with DMA/ISR preprocessing → Linux SBC _Rust_ service → record→analyze→replay tools → metrics dashboards.**

The aim isn’t a SOTA classifier; it’s **system engineering**: clear interfaces (UML/ICDs), timing budgets, and testability.

**Repo:** <https://github.com/aarzhoca/vr-wrist-emg-lab>
![GitHub Repo stars](https://img.shields.io/github/stars/aarzhoca/vr-wrist-emg-lab?style=social)
![License](https://img.shields.io/badge/license-MIT-blue.svg)
### What’s in the repo
- A host **Rust** service exposing `/ingest` and Prometheus `/metrics`
- **Record/replay** Python tools for deterministic debugging
- Text **UML/ICD** notes to align HW/FW/ML
- A firmware placeholder describing DMA/ISR capture, fixed-point preprocessing, and transport

### Quick start (host service)
```bash
cd host_rust_service
cargo run
# New shell:
python tools/record_replay/record.py --outfile data/run1.bin
python tools/record_replay/replay.py --infile data/run1.bin --endpoint http://localhost:9090/ingest
