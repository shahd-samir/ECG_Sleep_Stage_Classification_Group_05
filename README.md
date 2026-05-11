# Sleep Stage Classification using ECG & HRV Signals

A hybrid deep learning framework for automatic sleep stage classification using Electrocardiogram (ECG) signals and Heart Rate Variability (HRV) features.  
The project combines advanced signal preprocessing, HRV feature engineering, and deep neural network architectures including ResNet1D and Transformer Encoder models for robust multi-class sleep stage prediction.

---

# Project Overview

Sleep stage classification is a critical task in sleep medicine and clinical diagnosis. Traditional manual sleep scoring is time-consuming, labor-intensive, and subject to inter-observer variability.

This project introduces an automated deep learning pipeline capable of classifying sleep into five stages:

- Wake (W)
- N1
- N2
- N3
- REM

using:

- Raw ECG Signals
- HRV Physiological Features
- Deep CNN + Transformer Architecture

The proposed framework aims to provide a reliable and scalable alternative for automated sleep analysis systems.

---

# Proposed Architecture

The system uses a dual-input hybrid deep learning model consisting of two main branches:

## ECG Branch

- CNN Layers
- ResNet1D Backbone
- Dilated Convolutions
- Transformer Encoder
- Global Average Pooling

This branch learns deep temporal and morphological ECG representations.

## HRV Branch

- Fully Connected Dense Layers

This branch processes handcrafted physiological HRV features extracted from ECG signals.

## Fusion Layer

Features from both branches are fused before final classification using:

- Dense Layers
- Softmax Activation

---

# Dataset

The project uses data derived from the MESA Sleep Dataset.

## Dataset Structure

- Signals (.edf)
- Annotations (.nsrr)

## Data Information

| Property | Description |
|---|---|
| Signal Type | ECG |
| Format | EDF |
| Labels | Sleep Stages |
| Epoch Length | 30 seconds |

Each EDF file corresponds to one subject and contains ECG recordings with associated sleep stage annotations.

---

# Preprocessing Pipeline

The preprocessing stage includes several signal enhancement and preparation steps:

## Signal Filtering

A Butterworth Bandpass Filter was applied within the range:

```math
0.5 \, Hz \leq f \leq 40 \, Hz
```

This filtering process removes:

- Baseline drift
- High-frequency noise
- Motion artifacts

## Signal Segmentation

ECG recordings were segmented into:

```math
30\text{-second epochs}
```

Each epoch corresponds to one sleep stage label.

## HRV Feature Extraction

HRV features were extracted from RR intervals to capture autonomic nervous system activity.

## Robust Signal Normalization

Robust normalization techniques were applied to improve stability and reduce signal variability.

## Data Balancing & Augmentation

To address class imbalance:

- Minority classes were augmented
- Augmentation was applied only to the training set
- HRV features remained unchanged to preserve physiological consistency

This produced a more balanced dataset across all sleep stages.

---

# HRV Features

The extracted HRV features include:

## Time-Domain Features

- Mean RR Interval
- RMSSD
- SDNN
- pNN50

## Frequency-Domain Features

- LF Power
- HF Power
- LF/HF Ratio

## Nonlinear Features

- SD1
- SD2
- SD1/SD2 Ratio

---

# Hybrid Loss Function

The model uses a hybrid loss function combining:

- Focal Loss
- Label Smoothing Cross Entropy

Focal Loss parameter:

```math
\gamma = 3.0
```

Label smoothing factor:

```math
\alpha = 0.1
```

This improves:

- Minority class learning
- Model stability
- Generalization performance

---

# Training Configuration

| Parameter | Value |
|---|---|
| Optimizer | AdamW |
| Batch Size | 32 |
| Initial Learning Rate | 1e-3 |
| Fine-Tuning Learning Rate | 2e-5 |
| Initial Training | 10 Epochs |
| Fine-Tuning | 10 Epochs |

---

# Evaluation Metrics

The model was evaluated using:

- Accuracy
- Balanced Accuracy
- Precision
- Recall
- F1-Score
- Cohen’s Kappa
- ROC Curve
- Confusion Matrix

---

# Results

The proposed framework achieved strong performance in multi-class sleep stage classification by effectively combining:

- Deep ECG representations
- HRV physiological descriptors
- Transformer-based temporal modeling

## Model Performance

| Metric | Score |
|---|---|
| Test Accuracy | 79.70% |
| Balanced Accuracy | 73.39% |
| Cohen’s Kappa | 70.93% |
| Weighted F1-Score | 80.0% |

The model demonstrated:

- Stable convergence
- Good generalization on unseen data
- Balanced prediction behavior across sleep stages

The framework successfully distinguished between:

- Wake
- N1
- N2
- N3
- REM

---

# Model Strengths

- Hybrid ECG + HRV Learning
- ResNet1D + Transformer Encoder
- Strong Temporal Feature Extraction
- Balanced Training Strategy
- Robust Signal Processing Pipeline
- Improved Generalization using Augmentation

---

# Limitations

Despite strong performance, several limitations remain:

- Limited dataset size
- High computational requirements
- Sensitivity to R-peak detection accuracy
- Need for larger real-world datasets for stronger generalization

---

# Technologies & Libraries

## Programming Language

- Python

## Libraries

- TensorFlow / Keras
- NumPy
- Pandas
- SciPy
- Scikit-learn
- MNE
- Matplotlib
- Seaborn

---

# Workflow

```text
Raw ECG Signals
        ↓
Preprocessing & Filtering
        ↓
30s Segmentation
        ↓
HRV Feature Extraction
        ↓
Dual-Input Deep Learning Model
        ↓
Sleep Stage Prediction
```

To make the project more research-oriented and visually stronger, include:

- Architecture Diagram
- Complete Pipeline Diagram
- Confusion Matrix
- ROC Curve
- Training & Validation Curves

These visualizations significantly improve presentation quality and research credibility.

---

# Future Improvements

Possible future enhancements include:

- Using larger multi-center datasets
- Adding EEG and respiration signals
- Developing lightweight wearable models
- Applying self-supervised learning approaches
- Building real-time sleep monitoring systems

---

# Authors

## Group 05 – Biomedical Engineering

- Shahd Samir Shaaban
- Amany Mahmoud Bakry

## Supervisor

- Dr. Ibrahim Sadik
- Eng. Veronicaa William

---

# Conclusion

This project presents an effective hybrid deep learning framework for automatic sleep stage classification using ECG and HRV signals.

The integration of:

- ResNet1D
- Transformer Encoder
- HRV Physiological Features

provides reliable and robust classification capability, demonstrating strong potential for real-world clinical sleep analysis applications.
