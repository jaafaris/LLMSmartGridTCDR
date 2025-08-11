# DistilBERT — Fault vs. Attack (Main Case Study)

This repository contains a Jupyter notebook that fine-tunes DistilBERT to classify fault (0) vs attack (1) using current measurements from a line current differential relay (LCDR).

- Main case only: clean data, no noise, no time delay.
- Input file: `RelayMeasurementDataset.csv` (numeric, ready-to-use).
- The notebook converts each numeric sample to a descriptive text string internally and then trains DistilBERT.

---

## What the notebook does

1. Loads `RelayMeasurementDataset.csv` (numeric measurements + `label`)
2. Gives meaningful names to measurement columns (PhaseA/B/C × In/Out)
3. Converts each row (time × 6 channels) into a descriptive text
4. Splits the data into train/validation (stratified)
5. Tokenizes using `distilbert-base-uncased`
6. Fine-tunes DistilBERT with HuggingFace Trainer
7. Evaluates on the validation set (accuracy, precision, recall, F1, confusion matrix)
8. Saves the fine-tuned model, tokenizer, and predictions

---

## Requirements

- Python 3.9+ (recommended)
- Packages:
  - `transformers` (>= 4.30 recommended)
  - `torch`
  - `scikit-learn`
  - `pandas`
  - `numpy`
  - `matplotlib` (optional, for plots)

Install if needed:

```bash
pip install -U transformers torch scikit-learn pandas numpy matplotlib
