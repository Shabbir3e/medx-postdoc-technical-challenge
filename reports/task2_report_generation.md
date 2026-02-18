# Task 2: Medical Report Generation (Vision-to-Text Pipeline)

## 1. Objective

The objective of Task 2 is to design a system that generates structured medical reports from chest X-ray images.

Due to CPU-only constraints and limited paired image-text data, a lightweight yet clinically meaningful pipeline was implemented.

The system predicts pneumonia probability and generates a structured, interpretable clinical report conditioned on model confidence.

---

## 2. System Overview

The pipeline consists of:

1. Vision Encoder (ResNet18)
2. Probabilistic Classification Head
3. Structured Clinical Report Generator

This design separates visual understanding from language formulation for interpretability and efficiency.

---

## 3. Methodology

### 3.1 Vision Encoder

A pretrained **ResNet18** model was used as a frozen feature extractor.

- Input resolution: 128×128
- Grayscale images converted to 3-channel
- Final classification layer removed
- Output feature vector: 512 dimensions

The encoder was frozen to:
- Reduce training time
- Improve stability
- Leverage pretrained representations

---

### 3.2 Classification Head

A lightweight classifier was trained:

- Linear layer (512 → 1)
- BCEWithLogitsLoss
- Adam optimizer
- 2 training epochs

The model outputs:

\[
p(\text{pneumonia} \mid X\text{-ray})
\]

---

### 3.3 Structured Report Generation

Instead of training a full autoregressive language model (computationally expensive and unstable on small data), a structured template-based report generator was implemented.

Reports are conditioned on predicted probability:

| Probability Range | Interpretation |
|------------------|---------------|
| ≥ 0.70 | Pneumonia consistent |
| 0.40–0.69 | Indeterminate |
| < 0.40 | No evidence of pneumonia |

Each report includes:

- Findings section
- Impression section
- Model confidence score

This approach ensures interpretability and avoids hallucination risks common in generative models.

---

## 4. Quantitative Results

Test Set Performance:

- Accuracy: **0.8429**
- AUC: **0.9308**

The high AUC indicates strong separability between normal and pneumonia classes.

---

## 5. Example Output

Example (Test Image):


The generated report aligns with predicted probability and provides transparent confidence.

---

## 6. Discussion

While this is not a full transformer-based Vision-Language Model, the system demonstrates:

- Image feature extraction
- Probabilistic reasoning
- Clinically structured report generation
- Confidence-aware decision support
- Efficient CPU-compatible deployment

This modular design enhances interpretability compared to end-to-end black-box VLM systems.

---

## 7. Future Improvements

Potential extensions include:

- Fine-tuning the visual backbone
- Transformer-based autoregressive decoding
- Multi-sentence medical report generation
- Calibration analysis
- Uncertainty quantification

---

## 8. Conclusion

This task demonstrates a practical, interpretable, and computationally efficient approach to medical report generation.

The system successfully integrates visual representation learning with structured clinical language generation while maintaining strong classification performance (AUC ≈ 0.93).

