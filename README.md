# Beyond Accuracy: Uncertainty-Aware Hybrid Deep Learning for Reliable Infectious Disease Chest X-ray Classification in Low-Resource Settings

## Overview

This project investigates uncertainty-aware artificial intelligence for multiclass chest X-ray (CXR) classification of infectious pulmonary diseases in low-resource settings.

Building on a high-performing hybrid DenseNet-121 + Vision Transformer (ViT-Tiny) architecture, this study moves beyond accuracy by evaluating predictive uncertainty, calibration, and selective referral for safer clinical deployment.

The goal is not only to achieve strong classification performance, but also to determine whether the model can recognize when it is uncertain and should defer cases for expert radiologist review.

---

## Diseases Classified

* COVID-19
* Pneumonia
* Tuberculosis (TB)
* Normal Chest X-rays

---

## Dataset

### Nigerian Chest X-ray Dataset

Balanced multiclass dataset containing:

* 2,600 total images
* 4 disease classes
* 2,000 training images
* 600 testing images

### Per-Class Distribution

* 500 images/class for training
* 150 images/class for testing

Dataset source:

aminumusa/nigeria-chest-x-ray-dataset

---

## Model Architecture

This project uses a hybrid feature fusion architecture combining:

### 1. DenseNet-121

Captures strong local radiographic features such as:

* pulmonary opacities
* infiltrates
* consolidations
* cavitations

### 2. Vision Transformer (ViT-Tiny)

Captures:

* global contextual representations
* distributed attention patterns
* long-range dependencies across the chest radiograph

### 3. Fusion Classifier

Feature-level concatenation followed by:

* Fully connected layer
* ReLU activation
* Dropout (0.3)
* Final classification layer

This allows simultaneous learning of:

* local CNN features
* global transformer features

---

## Uncertainty Quantification

### Monte Carlo Dropout (MC Dropout)

Instead of a single prediction, dropout remains active during inference and the model performs:

### 30 stochastic forward passes per image

This provides:

* predictive confidence
* predictive entropy
* mean class probability
* uncertainty estimation
* variance across predictions

This helps answer:

### “How sure is the model?”

instead of only:

### “What is the prediction?”

---

## Evaluation Metrics

### Classification Metrics

* Accuracy
* Precision
* Recall
* F1-score
* Macro ROC-AUC
* Confusion Matrix

### Reliability Metrics

* Expected Calibration Error (ECE)
* Brier Score
* Predictive Entropy
* Confidence Analysis

### Clinical Safety Metrics

* Error vs Uncertainty Analysis
* Selective Prediction
* Human-in-the-loop Referral Analysis

---

## Results

### Baseline Hybrid Model

* Accuracy: 99.0%
* Macro AUC: 0.99959

### Uncertainty Findings

Wrong predictions showed:

* higher predictive entropy (0.2002 vs 0.0226)
* lower confidence (0.9261 vs 0.9930)

This demonstrates that the model meaningfully identifies uncertain and potentially unsafe predictions.

### Selective Prediction

When the most uncertain 15–20% of cases were referred for radiologist review:

* diagnostic accuracy improved from 99.0% to 100%

This supports safer human-in-the-loop deployment.

---

## Clinical Significance

High accuracy alone is not enough.

Reliable medical AI systems must also know when they are uncertain.

This is especially important in:

* low-resource hospitals
* infectious disease screening
* tuberculosis programs
* radiologist shortage environments

This system supports:

* safer automated triage
* selective expert referral
* improved trust in AI-assisted diagnosis

---

## Installation

```bash
pip install torch torchvision timm scikit-learn matplotlib numpy
```

---

## Project Structure

```text
my_dataset/

├── train_folder/
│   ├── COVID/
│   ├── NORMAL/
│   ├── PNEUMONIA/
│   └── TB/

└── test_folder/
    ├── COVID/
    ├── NORMAL/
    ├── PNEUMONIA/
    └── TB/
```

---

## Model Checkpoint

Load pretrained hybrid model using:

```python
model_path = "/content/drive/MyDrive/Vit Model/hybrid_densenet_vit_tiny.pth"
```

---

## Workflow

### Step 1

Prepare dataset folders

### Step 2

Load pretrained hybrid checkpoint

### Step 3

Run baseline evaluation

### Step 4

Apply Monte Carlo Dropout inference

### Step 5

Perform:

* uncertainty analysis
* calibration analysis
* selective prediction
* reliability evaluation

---

## Future Work

Future directions include:

* Deep Ensembles for stronger uncertainty estimation
* External validation across African hospitals
* Domain shift analysis across institutions
* Mammography adaptation for breast cancer imaging
* Clinical deployment via lightweight decision-support tools

---

## Author

### Jonathan Wisdom

Niger Delta University, Nigeria

### Research Interests

* Medical Imaging AI
* AI Safety and Trustworthiness
* Clinical Deep Learning
* Digital Health Governance
* AI for Low-Resource Health Systems

---

## Citation

If you use this work, please cite:

Wisdom, J.

Beyond Accuracy: Uncertainty-Aware Hybrid Deep Learning for Reliable Infectious Disease Chest X-ray Classification in Low-Resource Settings

ICID 2026 Submission (Under Review)

---

