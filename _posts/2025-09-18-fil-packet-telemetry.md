---
layout: post
title: "Firmware-in-the-Loop Packet Telemetry (MCU + SBC Classifier)"
---

Goal: connect MCU timing features with a tiny classifier on an SBC to label network conditions.

**Topology**
- Linux SBC replays pcaps → MCU gathers timing/flow features
- SBC runs a tiny sklearn/C++ model → sends advisory back (raise log level, dump buffer)

**Engineering notes**
- Back-pressure & buffering strategies
- ISR/RTOS scheduling and determinism
- CI: canned pcaps → golden outputs; sanitizer runs

**Artifacts**
- Link to repo (coming soon)
- Example telemetry and expected outputs
