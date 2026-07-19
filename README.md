# EnMSRCR: Enhanced Multi-Scale Retinex for Video Content Retrieval

**Deep Learning-Based Video Content Retrieval with Adaptive Illumination Enhancement**

**Undergraduate Thesis — Northwestern Polytechnical University (NWPU)**  
School of Mathematics and Statistics  

**Author:** Tsend-Ayush Ganbold   
**Advisor:** Prof. Wang Yong (王勇)

**Recognition:** Best Graduation Thesis Award, School of Mathematics and Statistics, NWPU (2026)  
**Defense Score:** 95.3 / 100  

---

# Project Overview

This repository contains the research artifacts for an undergraduate thesis investigating whether **MSRCR-based illumination preprocessing** improves the **stability and discriminability** of deep-feature keyframe selection in **Content-Based Video Retrieval (CBVR)** systems.

The proposed method, **EnMSRCR (Enhanced Multi-Scale Retinex with Color Restoration)**, extends standard MSRCR by introducing adaptive parameters based on image brightness and contrast characteristics.

## Research Question

> Can illumination enhancement improve deep feature-based video retrieval performance under challenging lighting conditions?

## Complete Pipeline

Video Frames
↓
EnMSRCR Illumination Enhancement
↓
ResNet-18 Feature Extraction
↓
K-means Keyframe Selection
↓
Similarity Retrieval & Evaluation

---

# Key Findings

| Result | Value |
|---|---|
| Clustering stability SD reduction (Standard MSRCR, normal lighting) | **40.8%** (0.0669 → 0.0396) |
| Low-light Precision@5 recovery (Standard MSRCR, f=0.4) | 0.960 → **0.980** |
| Bilateral Filter component effect on retrieval | **Cohen's d = −0.741**, p < .001 |
| Adaptive parameter components vs. Standard MSRCR | Statistically equivalent (p > .79) |

## Main Insight

MSRCR-based preprocessing significantly improves the **reproducibility of clustering-based keyframe selection** across independent runs.

The six-variant ablation study shows that:

- Adaptive parameter tuning provides a safe and backward-compatible extension of standard MSRCR.
- Bilateral-filter-based illumination estimation may improve visual appearance but negatively affects downstream ResNet-18 feature discriminability.

---

# Pipeline Architecture

The proposed framework integrates illumination enhancement before deep feature extraction:

**Frame Extraction → Preprocessing → ResNet-18 Feature Extraction → K-means Clustering → Retrieval Evaluation**

![CBVR Pipeline Architecture](figures/01_pipeline_architecture.png)

---

# EnMSRCR Algorithm

Standard MSRCR applies fixed parameters:

- α = 125
- β = 46
- σ ∈ {15, 80, 250}

However, fixed parameters cannot adapt to different illumination conditions.

EnMSRCR introduces adaptive strategies using brightness (μ_b) and contrast (σ_c):

## Adaptive Components

### 1. Adaptive α and β

Adjusts color restoration strength according to illumination conditions.

### 2. Bilateral Filter Illumination Estimation

Replaces Gaussian filtering while preserving edge information.

### 3. Adaptive Multi-scale σ

Adjusts illumination estimation scales based on image characteristics.

![EnMSRCR Flowchart](figures/02_enmsrcr_flowchart.png)

---

# Six-Variant Ablation Study

A six-variant ablation study was conducted to analyze the contribution of each adaptive component.

| ID | Variant | Observation |
|---|---|---|
| 1 | Baseline | Lower retrieval performance under low-light conditions |
| 2 | Standard MSRCR | Reference method |
| 3 | Adaptive α, β | Statistically equivalent (p = .844) |
| 4 | Bilateral Filter | **Significantly worse (d = −0.741, p < .001)** |
| 5 | Adaptive σ | Statistically equivalent (p = .796) |
| 6 | Full EnMSRCR | Influenced by Bilateral Filter limitation |

![Ablation Results](figures/03_ablation_results.png)

## Interpretation

The parameter-adaptive components are safe extensions of MSRCR.

However, Bilateral Filter-based illumination estimation can suppress texture information required by ResNet-18 feature extraction, demonstrating that improved visual quality does not always translate into improved retrieval performance.

---

# Feature Space Visualization

512-dimensional ResNet-18 feature representations were projected using PCA to visualize how preprocessing affects feature distributions under simulated low-light conditions.

Evaluated UCF11 categories:

- Basketball shooting
- Biking
- Diving
- Tennis swinging

![PCA Visualization](figures/04_pca_visualization.png)

Additional comparison under normal lighting conditions:

![PCA visualization under normal lighting](figures/05_pca_normal_visualization.png)
---

# Experimental Setup

## Dataset

**UCF11 (YouTube Action Dataset)**

- 40 video clips
- 4 action categories

## Deep Feature Extraction

- ResNet-18
- ImageNet pretrained model
- Frozen 512-dimensional GAP features

## Keyframe Selection

- K-means clustering
- Silhouette-based automatic K selection

## Evaluation Metrics

- Precision@5
- Silhouette Score
- Clustering Stability (Standard Deviation)

## Statistical Analysis

- Paired t-test
- Cohen's d Effect Size
- 95% Confidence Intervals
- One-way ANOVA
- Tukey HSD

## Environment

- Python 3.11
- PyTorch 2.9
- Windows 11
- Intel Core i5-1335U CPU

---

# Repository Structure

enmsrcr-video-retrieval/

├── README.md
├── LICENSE
│
├── figures/
│ ├── 01_pipeline_architecture.png
│ ├── 02_enmsrcr_flowchart.png
│ ├── 03_ablation_results.png
│ └── 04_pca_visualization.png
│
├── code/
│ └── implementation files
│
└── thesis

---

# Thesis Documentation

Full undergraduate thesis:

[View Thesis PDF](thesis/Tsend_Ayush_Ganbold_Bachelor_Thesis_EnMSRCR.pdf)

---

# Citation

If you reference this work:

└── Tsend_Ayush_Ganbold_Bachelor_Thesis_EnMSRCR.pdf
Tsend-Ayush, G. (2026).

Research on Video Content Retrieval Based on Deep Learning:
An Empirical Study of MSRCR-Enhanced Keyframe Selection.

Bachelor's Thesis,
Northwestern Polytechnical University,
School of Mathematics and Statistics.

Advisor: Prof. Wang Yong.

A follow-up manuscript based on this research is currently being prepared.

---

# Author

**Tsend-Ayush Ganbold**

B.Sc. in Statistics  
Northwestern Polytechnical University (NWPU)

Technical interests:

- Data Analysis
- Machine Learning
- Computer Vision
- Statistical Modeling

---

# License

This project is released under the MIT License.
