# Diff-Kalman

<p align="center">
  <b>Difference-Driven Learning for Structure-Preserving Kalman Filtering</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/NeurIPS-2026%20Main%20Track-6B4EFF" alt="NeurIPS 2026">
  <img src="https://img.shields.io/badge/Presentation-Poster-2F80ED" alt="Poster">
  <img src="https://img.shields.io/badge/Code-Coming%20Soon-lightgrey" alt="Code Coming Soon">
</p>

<p align="center">
  <a href="https://openreview.net/forum?id=kk5tmlhwi6">OpenReview</a>
  &nbsp;|&nbsp;
  <a href="https://github.com/heu-gj/Diff-Kalman">Repository</a>
</p>

---

## Overview

**Diff-Kalman** is a hybrid Kalman-style filtering framework that introduces **difference-driven corrections** in both the prediction and update phases while preserving the recursive predict-update structure.

Instead of directly predicting a full Kalman gain or covariance-related matrix, Diff-Kalman learns structured correction terms. In the prediction phase, it combines model-based dynamics with a learned state increment. In the update phase, it uses learned scaling to calibrate uncertainty and correct the Kalman gain.

The framework is designed for state-estimation problems with nonlinear dynamics, model mismatch, or inaccurate noise statistics.

## Method

Diff-Kalman contains two main phases.

### Prediction

Given historical states and their first-order differences:

1. A Transformer predicts a **neural state increment**.
2. **GSP-\(\alpha\)** fuses the neural increment with the **model-based increment**.
3. **GSP-P** calibrates the model-propagated uncertainty while preserving its positive-semidefinite form.

### Update

Given the current innovation and prior uncertainty:

1. **GSP-K** generates a structured scaling factor.
2. The scaling is used to correct the Kalman gain.
3. The corrected gain is used in the recursive state update.

A compact view of the pipeline is:

```text
Historical states + state differences
                │
                ▼
           Transformer
                │
                ▼
       Neural state increment
                │
                ├──────────────┐
                │              │
                ▼              ▼
             GSP-α      Model-based increment
                │              │
                └──────┬───────┘
                       ▼
              Corrected prior state
                       │
             ┌─────────┴─────────┐
             ▼                   ▼
           GSP-P              Innovation
             │                   │
             ▼                   ▼
  Calibrated prior uncertainty  GSP-K
             │                   │
             └─────────┬─────────┘
                       ▼
               Corrected Kalman gain
                       │
                       ▼
                Posterior estimate
```

## Key Features

- **Difference-driven prediction.** State differences are used to model local dynamics and predict state increments.
- **Model-data fusion.** Learned increments are fused with model-based increments rather than replacing the dynamic model.
- **Structured uncertainty calibration.** GSP-P rescales the model-propagated uncertainty while preserving positive semidefiniteness.
- **Gain correction.** GSP-K applies structured scaling to the Kalman gain based on the innovation and prior uncertainty.
- **Recursive filtering structure.** The method retains a Kalman-style prediction-update recursion instead of replacing the filter with an unconstrained end-to-end network.

## Experiments

The current manuscript evaluates Diff-Kalman on:

- **MOT trajectories** extracted from MOT17 for linear state estimation.
- **Lorenz dynamics** for nonlinear and chaotic state estimation.

The experiments compare Diff-Kalman with classical filters and learning-based Kalman methods, and include ablation and robustness studies.

Additional experiments and the final camera-ready results will be reflected in this repository.

## Repository Status

This repository is being prepared for the camera-ready release.

- [x] NeurIPS 2026 Main Track acceptance
- [x] Project repository
- [ ] Camera-ready paper
- [ ] Training code
- [ ] Evaluation code
- [ ] Configuration files
- [ ] Pretrained checkpoints
- [ ] Reproduction scripts

> **Code release.** The implementation is currently being cleaned and documented. Training and evaluation code, configurations, and reproduction instructions will be released with the final version.

## Reproducibility

The experiments in the manuscript were conducted with:

- Python 3.10
- PyTorch 2.5.1
- CUDA 12.1
- NVIDIA GeForce RTX 4090 D

Exact environments, random seeds, dataset preparation scripts, and evaluation commands will be included in the code release.

## Citation

Citation information will be updated when the camera-ready version is available.

## Contact

For questions about the paper or implementation, please open an issue in this repository.

---

If you find this work useful, please consider starring the repository. ⭐
