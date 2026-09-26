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

## News

- **Sep. 2026:** Diff-Kalman was accepted to the **NeurIPS 2026 Main Track** as a poster.
- **Code release:** The implementation is being cleaned and documented for public release.

## Overview

**Diff-Kalman** is a hybrid Kalman-style filtering framework that introduces **difference-driven corrections** in both the prediction and update phases while preserving the recursive predict-update structure.

Rather than directly predicting a full Kalman gain or an unrestricted uncertainty matrix, Diff-Kalman learns structured correction terms:

- **GSP-α** fuses a Transformer-predicted state increment with the model-based increment.
- **GSP-P** calibrates model-propagated uncertainty while preserving its positive-semidefinite form.
- **GSP-K** corrects the Kalman gain through structured scaling based on the innovation and prior uncertainty.

The framework is designed for state-estimation problems with nonlinear dynamics, model mismatch, or inaccurate noise statistics.

## Method

Diff-Kalman contains two main phases.

### Prediction Phase

1. A Transformer models historical states and their first-order differences.
2. The Transformer predicts a **neural state increment**.
3. **GSP-α** fuses the neural increment with the **model-based increment**.
4. **GSP-P** calibrates the model-propagated uncertainty.

### Update Phase

1. The current observation produces the innovation.
2. **GSP-K** generates a structured scaling factor from the innovation and prior uncertainty.
3. The scaling corrects the Kalman gain.
4. The corrected gain is used in the recursive state update.

A compact view of the pipeline is:

```text
Historical states + state differences
                |
                v
           Transformer
                |
                v
       Neural state increment
                |
                +----------------+
                |                |
                v                v
             GSP-α      Model-based increment
                |                |
                +-------+--------+
                        |
                        v
               Corrected prior state
                        |
              +---------+---------+
              |                   |
              v                   v
            GSP-P             Innovation
              |                   |
              v                   v
 Calibrated prior uncertainty   GSP-K
              |                   |
              +---------+---------+
                        |
                        v
                Corrected Kalman gain
                        |
                        v
                 Posterior estimate
```

## Experiments

The current manuscript evaluates Diff-Kalman on:

- **MOT trajectories** extracted from MOT17 for linear state estimation.
- **Lorenz dynamics** for nonlinear and chaotic state estimation.

The paper includes comparisons with classical and learning-based filtering methods, as well as ablation and robustness studies.

Camera-ready experiments and the corresponding reproduction scripts will be added to this repository with the public code release.

## Code Release Status

- [x] NeurIPS 2026 Main Track acceptance
- [x] Public project repository
- [ ] Camera-ready paper
- [ ] Environment file
- [ ] Training code
- [ ] Evaluation code
- [ ] Dataset preparation scripts
- [ ] Configuration files
- [ ] Pretrained checkpoints
- [ ] Table/figure reproduction scripts

## Installation

Installation instructions will be added with the code release.

The experiments in the current manuscript use:

- Python 3.10
- PyTorch 2.5.1
- CUDA 12.1

## Data Preparation

Dataset preparation instructions will be provided for each experiment at release.

## Training and Evaluation

Training and evaluation commands will be documented once the code is public. We will provide separate entry points or configuration files for the main experimental settings.

## Reproducing the Paper

The release will include the scripts and configurations needed to reproduce the main tables and figures reported in the camera-ready paper.

## Citation

Citation information will be added after the camera-ready metadata is finalized.

## Contact

For questions about the paper, code, or reproducibility, please open an issue in this repository.

---

If you find this work useful, please consider starring the repository. ⭐
