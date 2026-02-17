
This provided the best trade-off between sensitivity and specificity.

---

## 5. Test Set Performance

Final test performance using threshold = 0.51:

- Accuracy: **0.8718**
- Precision: **0.8370**
- Recall (Sensitivity): **0.9872**
- F1-score: **0.9059**
- AUC: **0.9608**
- Specificity: **0.6795**

Confusion Matrix:

|               | Pred Normal | Pred Pneumonia |
|---------------|------------|----------------|
| True Normal   | 159        | 75             |
| True Pneumonia| 5          | 385            |

---

## 6. Interpretation of Results

### AUC = 0.9608

The high AUC indicates strong separability between normal and pneumonia classes.

### High Recall (0.9872)

The model correctly identifies nearly all pneumonia cases. Only 5 false negatives were observed. This is desirable in a clinical screening setting, where missing pneumonia cases can have severe consequences.

### Moderate Specificity (0.6795)

The model still produces false positives (75 normal cases classified as pneumonia). This reflects a conservative operating point favoring sensitivity over specificity.

### Trade-Off

The selected threshold prioritizes sensitivity while maintaining acceptable specificity, making it suitable for screening applications where over-referral is preferable to missed diagnoses.

---

## 7. Failure Case Analysis

### False Positives (Normal → Pneumonia)

Observed patterns:
- Mild brightness variations
- Low-contrast regions
- Hazy lung areas
- Downsampling artifacts due to 28×28 resolution

Because images are heavily downsampled, fine anatomical detail is lost. The model relies primarily on global intensity distribution and coarse structural cues, which may resemble pneumonia-like opacities.

### False Negatives (Pneumonia → Normal)

Only 5 cases were missed. These typically exhibited:
- Subtle or localized pneumonia features
- Low contrast patterns
- Possibly mild disease presentation

---

## 8. Limitations

1. Very low image resolution (28×28) limits anatomical detail.
2. No advanced data augmentation (e.g., elastic transforms).
3. Model does not incorporate attention mechanisms.
4. No external validation beyond provided dataset.

---

## 9. Conclusion

A compact CNN with imbalance handling and validation-based threshold tuning achieved strong performance:

- AUC ≈ 0.96
- F1 ≈ 0.91
- Near-perfect sensitivity

The model demonstrates robust pneumonia detection capability with clinically favorable sensitivity–specificity trade-offs.

Future work could explore:
- Higher resolution training
- Attention-based models
- Multi-scale feature extraction
- Calibration analysis

---

## Figures

- `outputs/figures/confusion_matrix.png`
- `outputs/figures/false_positives.png`
- `outputs/figures/false_negatives.png`
