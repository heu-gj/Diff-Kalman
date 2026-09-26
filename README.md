# Diff-Kalman

<p align="center">
  <b>Difference-Driven Learning for Structure-Preserving Kalman Filtering</b>
</p>

<p align="center">
  <b>NeurIPS 2026 Main Track (Poster)</b>
</p>

<p align="center">
  <a href="https://openreview.net/forum?id=kk5tmlhwi6">Paper</a>
  &nbsp;|&nbsp;
  <a href="https://github.com/heu-gj/Diff-Kalman">Code (Coming Soon)</a>
</p>

---

## TL;DR

**Diff-Kalman** is a hybrid Kalman-style filtering framework that introduces difference-driven corrections in both the prediction and update phases while preserving the recursive predict-update structure.

## News

- **Sep. 2026** — Diff-Kalman was accepted to the **NeurIPS 2026 Main Track** as a poster.
- **Code release** — We are cleaning and documenting the implementation for public release.

## Overview

Diff-Kalman combines model-based filtering with learned corrections rather than directly predicting a full Kalman gain or an unrestricted uncertainty matrix.

The framework contains three learned components:

- **GSP-α** fuses a Transformer-predicted state increment with the model-based increment.
- **GSP-P** calibrates model-propagated uncertainty while preserving its positive-semidefinite form.
- **GSP-K** corrects the Kalman gain through structured scaling based on the innovation and prior uncertainty.

The same recursive prediction-update structure is retained throughout the filtering process.

## Method

### Prediction phase

A Transformer models historical states and their first-order differences to predict a state increment.  
**GSP-α** fuses the learned increment with the model-based increment.  
**GSP-P** then calibrates the model-propagated uncertainty.

### Update phase

The current observation is used to compute the innovation.  
**GSP-K** uses the innovation and prior uncertainty to correct the Kalman gain through structured scaling.  
The corrected gain is then used in the recursive state update.

## Experiments

The current manuscript evaluates Diff-Kalman on:

- **MOT trajectories (MOT17)** for linear state estimation.
- **Lorenz dynamics** for nonlinear and chaotic state estimation.

The paper includes comparisons with classical and learning-based filtering methods, together with ablation and robustness studies.

Camera-ready experiments and reproduction scripts will be reflected in this repository when the code is released.

## Code Release

The public release will include the code and configurations needed to reproduce the main experiments in the paper.

- [x] Project repository
- [x] NeurIPS 2026 acceptance information
- [ ] Environment and dependency files
- [ ] Training code
- [ ] Evaluation code
- [ ] Dataset preparation scripts
- [ ] Experiment configurations
- [ ] Pretrained checkpoints
- [ ] Table and figure reproduction scripts

## Installation

Installation instructions will be provided with the public code release.

The current experiments use:

- Python 3.10
- PyTorch 2.5.1
- CUDA 12.1

## Data Preparation

Dataset download and preprocessing instructions will be provided for each experiment at release.

## Training

Training commands and configuration examples will be added with the code release.

## Evaluation

Evaluation commands and pretrained checkpoints will be added with the code release.

## Reproducing the Paper

We plan to provide dedicated scripts or configurations for reproducing the main tables and figures in the camera-ready paper.

## Citation

If you find this work useful, please consider citing our paper. BibTeX will be added after the camera-ready metadata is finalized.

## License

License information will be added with the public code release.

## Contact

For questions about the paper, implementation, or reproducibility, please open an issue in this repository.
