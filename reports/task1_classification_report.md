# Task 1: PneumoniaMNIST Binary Classification

## 1. Objective

The goal of this task is to develop a binary classifier for the PneumoniaMNIST dataset (28×28 grayscale chest X-ray images) to distinguish between:

- Class 0: Normal
- Class 1: Pneumonia

The task includes model development, experimental evaluation, threshold selection, and failure case analysis.

---

## 2. Dataset Overview

- Image resolution: 28×28 pixels (grayscale)
- Training samples: 4708
- Validation samples: 524
- Test samples: 624
- Binary classification (Normal vs Pneumonia)

Due to the low resolution (28×28), fine anatomical structures are heavily compressed, requiring the model to rely on global intensity and coarse structural features.

---

## 3. Model Architecture

A lightweight convolutional neural network (CNN) was implemented with the following structure:

- Conv2D (1→32) + BatchNorm + ReLU + MaxPool
- Conv2D (32→64) + BatchNorm + ReLU + MaxPool
- Conv2D (64→128) + BatchNorm + ReLU
- Adaptive Average Pooling
- Dropout (0.3)
- Fully Connected (128→1)

Loss function:
- `BCEWithLogitsLoss` with class imbalance handling via `pos_weight`

Optimizer:
- Adam (lr = 1e-3)
- Weight decay = 1e-4
- ReduceLROnPlateau scheduler

Data preprocessing:
- Random horizontal flip (train only)
- Normalization (mean=0.5, std=0.5)

---

## 4. Threshold Selection Strategy

Rather than using the default 0.5 threshold, threshold tuning was performed on the validation set.

Two criteria were evaluated:

- F1-score maximization
- Balanced accuracy maximization

The final selected threshold was:

