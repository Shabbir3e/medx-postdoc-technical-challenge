# MedX Postdoctoral Technical Challenge

This repository contains my submission for the MedX technical challenge, including medical image classification and semantic retrieval experiments using PneumoniaMNIST.

---

## Repository Structure

- `notebooks/`  
  Jupyter notebooks implementing Task 1 and Task 3.

- `reports/`  
  Written technical analysis and methodology descriptions.

- `outputs/figures/`  
  Evaluation plots and retrieval examples.

---

# Task 1 — Pneumonia Classification

Binary classification of Pneumonia vs Normal chest X-rays using a CNN trained on PneumoniaMNIST.

### Model
- 3-layer CNN with BatchNorm and Dropout
- BCEWithLogitsLoss
- Threshold tuning on validation set
- AUC and F1 optimization

### Test Performance

- Accuracy: **0.8718**
- Precision: **0.8370**
- Recall: **0.9872**
- F1-score: **0.9059**
- AUC: **0.9608**
- Specificity: **0.6795**

See:
- `reports/task1_classification_report.md`
- Confusion matrix in `outputs/figures/confusion_matrix.png`

---

# Task 3 — Semantic Retrieval System

A FAISS-based similarity search system built using embeddings extracted from the trained CNN backbone.

### Method
- 128-dimensional embeddings from penultimate CNN layer
- L2 normalization
- FAISS `IndexFlatIP` for cosine similarity retrieval
- Relevance defined as same ground-truth class

### Retrieval Performance (Test Set)

- Precision@1: **0.8926**
- Precision@3: **0.8974**
- Precision@5: **0.8952**
- Precision@10: **0.8902**

Retrieval example:
- `outputs/figures/task3_retrieval_example.png`

---

## Summary

This submission demonstrates:

- Supervised medical image classification
- Embedding-based similarity learning
- FAISS indexing for efficient retrieval
- Quantitative and qualitative evaluation
- Clean experimental organization and reproducibility
