# DistilBERT for Cyberattack Detection on Transformer Current Differential Relays (TCDRs)

## Problem Overview
Modern smart grid substations rely on Transformer Current Differential Relays (TCDRs) to protect critical transformers by measuring currents from both sides of the transformer. These measurements are used to detect internal faults.  
However, malicious actors can manipulate these measurements through **false tripping cyberattacks**, causing unnecessary transformer outages and threatening grid stability.  
The challenge is to reliably distinguish between **true fault conditions** and **malicious attacks** while ensuring no degradation of the relay’s original protection function.

---

## Dataset
The dataset was generated using an IEEE Power System Relaying Committee benchmark transmission system simulated in OPAL-RT HYPERSIM.

- **Cases:** ~50,000 samples (faults and cyberattacks)  
- **Measurements:** Six current waveforms (three phases per transformer side)  
- **Sampling Rate:** 1600 samples/sec  
- **Duration:** 20 ms per case  
- **Labels:** `0` = Fault, `1` = Cyberattack  

For the DistilBERT-based approach, each case is **converted into a textual description** before training. Example format:


---

## Solution Approach
We adapt **DistilBERT**, a compact Transformer-based language model, for binary classification of the textualized TCDR measurements.

### Steps
1. **Data Preprocessing**
   - Measurements converted into descriptive text format
   - Tokenization with `distilbert-base-uncased` tokenizer
2. **Model**
   - Pre-trained DistilBERT from Hugging Face
   - Fine-tuned for binary classification (`Fault` vs `Cyberattack`)
3. **Training Setup**
   - Learning rate: `2e-5`
   - Batch size: `16`
   - Epochs: `10`
   - Weight decay: `0.01`
   - Early stopping on validation performance
4. **Evaluation Metrics**
   - Accuracy
   - Precision
   - Recall
   - F1-score
   - Specificity

---

## Key Result (Main Case Study)
| Model        | Cyberattack Detection (%) | Accuracy (%) | F1-Score (%) |
|--------------|---------------------------|--------------|--------------|
| DistilBERT   | **94.96**                  | 99.64        | 99.64        |

---

## Requirements
```bash
python>=3.8
transformers>=4.53.1
torch>=1.10.0
scikit-learn
pandas




@article{DistilBERT_TCDR_2025,
  title={Large Language Models for Detecting Cyberattacks on Smart Grid Protective Relays},
  author={Ahmad Mohammad Saber and Paul Budnarain and Saeed Jafari and Zhengmao Ouyang and Amr Youssef and Deepa Kundur},
  journal={IEEE Letters},
  year={2025}
}

