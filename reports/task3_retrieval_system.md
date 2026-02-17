# Task 3: Semantic Retrieval System (PneumoniaMNIST)

## 1. Objective

This task builds a semantic retrieval system for PneumoniaMNIST using learned image embeddings.  
Given a query image, the system retrieves the top-k most similar images and evaluates retrieval quality using Precision@k.

Relevance definition:
- A retrieved image is considered relevant if it has the **same class label** (Normal / Pneumonia) as the query.

---

## 2. Embedding Model

Embeddings are extracted from the CNN trained in Task 1.

- Backbone: CNN trained for Pneumonia classification
- Embedding layer: **Flatten output (128-D)** before the final classification layer
- Normalization: L2 normalization applied to embeddings to enable cosine-similarity style retrieval

This approach leverages supervised learning to create a feature space where images with similar pathology should cluster together.

---

## 3. Indexing and Similarity Search

- Index: FAISS `IndexFlatIP` (Inner Product)
- Similarity: Inner product over **L2-normalized embeddings**, equivalent to cosine similarity
- Dataset indexed: Test set embeddings (N = 624)

---

## 4. Quantitative Results

Precision@k (Test set):

- Precision@1: **0.8926**
- Precision@3: **0.8974**
- Precision@5: **0.8952**
- Precision@10: **0.8902**

These values indicate that most retrieved neighbors share the same label as the query, showing that the embedding space preserves clinically meaningful similarity.

---

## 5. Qualitative Analysis

A qualitative retrieval example is saved in:

- `outputs/figures/task3_retrieval_example.png`

In typical cases:
- Pneumonia queries retrieve visually similar pneumonia-like patterns (diffuse opacity / low contrast)
- Normal queries retrieve clean lung fields

Failure cases (when mismatches occur) are likely due to:
- Extremely low resolution (28×28) removing fine anatomical detail
- Normal images with noise/brightness variations resembling mild pneumonia patterns
- Overlapping visual appearance between mild pneumonia and normal samples after downsampling

---

## 6. Conclusion

A supervised CNN embedding approach combined with FAISS indexing provides an efficient and accurate semantic retrieval system for PneumoniaMNIST, achieving ~0.89 Precision@k across multiple k values. This demonstrates that the learned representation is suitable not only for classification but also for similarity-based retrieval and dataset exploration.


