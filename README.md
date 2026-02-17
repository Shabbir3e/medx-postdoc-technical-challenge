# MedX Postdoctoral Technical Challenge

This repository contains my submission for the MedX technical challenge.

## Structure

- `notebooks/` → Jupyter notebooks for each task
- `reports/` → Written technical reports
- `outputs/figures/` → Evaluation and retrieval figures

---

## Task 1 — Pneumonia Classification

CNN-based binary classification of PneumoniaMNIST.

Test Performance:
- Accuracy: 0.8718
- Precision: 0.8370
- Recall: 0.9872
- F1-score: 0.9059
- AUC: 0.9608

See:
- `reports/task1_classification_report.md`
- Confusion matrix in `outputs/figures/`

---

## Task 3 — Semantic Retrieval

Embedding-based image retrieval using FAISS.

Precision@k:
- Precision@1: 0.8926
- Precision@3: 0.8974
- Precision@5: 0.8952
- Precision@10: 0.8902

Retrieval example:
- `outputs/figures/task3_retrieval_example.png`

---

This submission demonstrates:
- Supervised medical image classification
- Embedding-based similarity retrieval
- Structured experimentation and evaluation
