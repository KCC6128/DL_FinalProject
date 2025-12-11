# Drug–Disease Association Prediction  
Hybrid Machine Learning + Multi-Modal Deep Neural Network (MM-DNN)

This project predicts whether a drug can treat a specific disease using chemical
structure features, protein targets, and disease identity.  
We evaluate traditional machine learning baselines and propose a multi-modal
deep neural network (MM-DNN) that achieves the best performance.

---

## Overview

Drug repositioning aims to find new therapeutic uses for existing drugs, offering
a faster and more cost-effective alternative to traditional drug development.

This project includes:

- Dataset construction with **negative sampling**
- Feature engineering for drugs and diseases
- Baseline ML models (LR, RF, XGBoost)
- A **Two-Tower MM-DNN** for nonlinear drug–disease interaction learning

---

## Dataset

Source: https://www.kaggle.com/datasets/ariasha/drug-repositioning

| File | Description |
|------|-------------|
| `drugsInfo.csv` | Drug SMILES, targets, metadata |
| `diseasesInfo.csv` | Disease names and categories |
| `mapping.csv` | Known drug–disease associations |

Dataset size:

- 1410 drugs  
- 1573 diseases  
- 42,200 positive associations  

---

## Problem Definition

Binary classification task:


---

## Feature Engineering

### Drug Features
- **Morgan Fingerprints (1024 bits)** from SMILES  
- **Protein Target Multi-Hot Encoding**

### Disease Features
- Machine Learning models: **One-Hot**
- MM-DNN: **Embedding Layer** (learns semantic disease vectors)

---

## Negative Sampling Strategy

The dataset contains only positive associations.  
To create a balanced dataset:

- For each drug, sample diseases **not associated** with it  
- Maintain a **1:1 ratio** of positive/negative samples  
- Prevents trivial predictions (e.g., predicting all 1's)

---

## Models Implemented

### Baseline Machine Learning Models
- Logistic Regression  
- Random Forest  
- XGBoost  

### Multi-Modal DNN (MM-DNN)

Two-Tower neural architecture:

- **Drug Tower:** Dense layers on fingerprint + target features  
- **Disease Tower:** Embedding layer  
- **Fusion Layer:** Concatenate + Dense for final prediction  

---

## Results

| Model | AUC |
|-------|------|
| Logistic Regression | 0.8396 |
| Random Forest | 0.8294 |
| XGBoost | Lower (struggles with sparse FP) |
| **MM-DNN (Ours)** | **0.8508 — Best** |

Visualizations included:

- ROC Curve  
- Confusion Matrix  
- PCA feature space  
- XGBoost Feature Importance  

---

## How to Run

### Install dependencies
```bash
pip install rdkit-pypi xgboost tensorflow

