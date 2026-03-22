# CyberShield

**CyberShield** is a machine learning-based Intrusion Detection System (IDS) designed to detect network attacks in real-time network traffic.

> ⚠️ **Important:** The primary focus of this model is detecting attacks (`1`) rather than normal traffic (`0`). The dataset is heavily imbalanced, so the model is optimized to maximize detection of attacks.

---

## Table of Contents

- [Project Description](#project-description)
- [Repository Structure](#repository-structure)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Threshold Tuning](#threshold-tuning)
- [Notes](#notes)
- [Author](#author)

---

## Project Description

CyberShield uses a deep learning model to classify network traffic into **attacks** (`1`) and **normal traffic** (`0`). While it can attempt to classify the type of attack, the **priority is to identify attacks reliably**. This is particularly important for imbalanced datasets, where normal traffic is minimal compared to attack traffic.

---

## Repository Structure

| File | Description |
|------|-------------|
| `CyberShield.ipynb` | Main notebook for training and evaluating the IDS model. |
| `my_model.keras` | Saved Keras model for prediction. |
| `test_model.ipynb` | Notebook for testing the model on new network data. |
| `README.md` | This file, explaining usage and project details. |
| `requirements.txt` | Python dependencies needed to run the notebooks and model. |

---

## Features

- Detects attacks (`1`) in network traffic with high accuracy.  
- Attempts to classify the type of attack, but detection of attacks is the priority.  
- Threshold tuning available to adjust sensitivity (e.g., 0.3, 0.5, 0.6).  
- Handles large-scale datasets efficiently (up to 9 million rows).  

---

## Installation

1. Clone the repository:

```bash
git clone https://github.com/Yousef-salah-Ma/CyberShield.git
cd CyberShield
```
Install required Python libraries:
```bash
pip install -r requirements.txt
```
Ensure you have Python 3.9+ and TensorFlow/Keras installed to load the model.

Usage
Load and predict using the saved model:
```bash
from tensorflow.keras.models import load_model
import numpy as np

# Load the pre-trained model
model = load_model("my_model.keras")

# Example input (replace with your network traffic features)
X_sample = np.array([[...]])  # shape should match training features

# Predict probabilities
predictions = model.predict(X_sample)

# Convert to binary attack detection (0 = normal, 1 = attack)
threshold = 0.6
is_attack = (predictions > threshold).astype(int)

print("Attack Detected:" if is_attack[0][0] == 1 else "Normal Traffic")
```
Threshold Tuning

Adjusting the threshold can improve detection of attacks while reducing false positives:

Threshold
| Threshold | Notes                                                                  |
| --------- | ---------------------------------------------------------------------- |
| 0.3       | Very sensitive, detects most attacks but may give more false positives |
| 0.5       | Balanced sensitivity                                                   |
| 0.6       | Less sensitive, fewer false positives but may miss small attacks       |

Notes
The dataset is highly imbalanced: attack traffic (1) dominates, and normal traffic (0) is very low.
The model is optimized to prioritize detecting attacks, which is the critical requirement.
Using oversampling techniques like SMOTE would create extremely large datasets (40–50M rows), which is not feasible with current resources.
Focus first on detecting attacks; classifying the exact attack type can be improved later with more balanced data.

Author
Yousef Salah – Machine Learning & Cybersecurity Enthusiast
GitHub: @Yousef-salah-Ma
