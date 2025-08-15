LC# Large Language Models for Detecting Cyberattacks on Smart Grid Protective Relays - Dataset

This repository contains the dataset and code used in the experiments of our IEEE Transactions on Smart Grid letter:

# Citation 
Ahmad Mohammad Saber, Paul Budnarain, Saeed Jafari, Zhengmao Ouyang, Amr Youssef, and Deepa Kundur,
**"Large Language Models for Detecting Cyberattacks on Smart Grid Protective Relays,"**
 IEEE Open Access Journal of Power and Energy, 2025.

# Dataset File
The dataset is provided as a CSV file:

RelayMeasurementDataset.csv

Dataset Link: https://drive.google.com/drive/folders/1BIEkicBhP3yOnGkJGQEnh84GnmtZuwcu?usp=drive_link


## Problem Description
This repository implements a **DistilBERT-based classification pipeline** for detecting **faults** and **false data injection attacks (FDIAs)** in **Transformer current differential relays (TCDRs)** in smart grids.  
The aim is to identify cyber-attacks that mimic legitimate faults, which could otherwise mislead protection systems.

This work corresponds to the **main case study** from our research paper (see Citation), using clean measurement data only — no artificial noise or time delay perturbations.

## Dataset
The dataset used is `RelayMeasurementDataset.csv`, prepared from real-time relay simulation outputs.

- **Features:** 6 channels of relay current measurements:
  - `PhaseA_In`, `PhaseB_In`, `PhaseC_In` (transformer input side)  
  - `PhaseA_Out`, `PhaseB_Out`, `PhaseC_Out` (transformer output side)  
- **Time steps:** 32 per channel (downsampled from original 95 in an internal preprocessing step, not included here)
- **Labels:**  
  - `0` → Fault  
  - `1` → Attack  
- **Format in this repository:** Each sample is converted into a **textual description** of current values for each channel, suitable for DistilBERT tokenization.

Example (shortened):
   - Transformer Differential Relay's current measurement vector of phase A in transformer input side: [0.12 0.15 ...] Transformer Differential Relay's current measurement vector of phase B ...


> **Note:** This dataset represents only the clean case study without noise or delay.

## Approach
The classification pipeline follows these steps:

1. **Load dataset** from CSV (with `text` and `label` columns).
2. **Tokenize text data** using `DistilBertTokenizer` with truncation and padding (`max_length=512`).
3. **Create PyTorch datasets** for training and evaluation.
4. **Fine-tune DistilBERT** (`distilbert-base-uncased`) on the training set for binary classification.
5. **Evaluate** using accuracy, precision, recall, and F1-score on the clean test set.

The model learns to interpret numeric measurement sequences embedded in descriptive text.

## How to Run
1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/smartgrid-distilbert.git
   cd smartgrid-distilbert

## Install dependencies
   - pip install -r requirements.txt
   - Place RelayMeasurementDataset.csv in the project root.
   - Run the notebook


## Dataset License
This dataset is released for academic and non-commercial research use only.

Use is permitted only if the paper below is cited.

Commercial use is not allowed without prior written approval from the first author (Ahmad Mohammad Saber).


## How to Cite
If you use this dataset in your work, please cite the following paper:

**Plantext:**

A. M. Saber, P. Budnarain, S. Jafari, Z. Ouyang, A. Youssef, and D. Kundur,
"Large Language Models for Detecting Cyberattacks on Smart Grid Protective Relays,"
IEEE Open Access Journal of Power and Energy, 2025.

**BibTeX Citation:**

```bibtex
@article{saber2025llm_tcdr,
  author    = {Ahmad Mohammad Saber and Paul Budnarain and Saeed Jafari and Zhengmao Ouyang and Amr Youssef and Deepa Kundur},
  title     = {Large Language Models for Detecting Cyberattacks on Smart Grid Protective Relays},
  journal   = {IEEE Open Access Journal of Power and Energy},
  year      = {2025},
}

