# Vision Transformer for Early Prediction of Alzheimer’s Disease

## Acknowledgement

I would like to extend my sincere thanks to my Mentor Dr. Vidivelli S, and SASTRA Deemed University, for guiding me and providing me with resources upon successful completion of this project.

This project implements a **Vision Transformer (ViT)** model for the early diagnosis of **Alzheimer’s disease** using **brain MRI scans**. It leverages the power of transformer-based deep learning to accurately classify disease stages and aims to improve medical decision-making by enabling earlier detection.

---

## Objective

The goal is to build a diagnostic AI framework for **early-stage Alzheimer’s detection** using axial MRI slices. Vision Transformers (ViTs) are used instead of traditional CNNs to better capture **global contextual features** in medical images.

The model classifies images into **four cognitive stages**:
- No Impairment
- Very Mild Impairment
- Mild Impairment
- Moderate Impairment

Techniques such as **CLAHE enhancement**, **data augmentation**, and **learning rate scheduling** are used to improve model robustness.

---

## Dataset Overview

We use a **balanced and high-quality MRI dataset** that includes both real and synthetic scans, specifically curated for Alzheimer's classification.

### Dataset Source:
- **Kaggle**: [Best Alzheimer MRI Dataset – 99% Accuracy](https://www.kaggle.com/datasets/lukechugh/best-alzheimer-mri-dataset-99-accuracy)

### Dataset Highlights:
- Synthetic + Real MRI data generated via **Wasserstein GAN with Gradient Penalty (WGAN-GP)**
- **Balanced across 4 classes** with 2,560 samples per class
- **Metrics**:
  - FID: `0.13` (lower is better)
  - SSIM: `0.97`
  - PSNR: `32 dB`
  - Sharpness Difference: `0.04`

These metrics confirm the synthetic MRIs closely resemble real scans, improving classification performance for minority classes by **91.4%**.

### Data Properties:
- Image Size: `224 × 224 × 3`
- Classes: `4`
- Patch Size: `16`
- Latent Size: `768`
- Mean: `(0.485, 0.456, 0.406)`
- Std Dev: `(0.229, 0.224, 0.225)`

---

## Vision Transformer Architecture

The model follows the **ViT-B/16** architecture with no pretrained weights.

### Key Components:
- **Image Patching**: Images are divided into `16x16` non-overlapping patches.
- **Linear Projection**: Each patch is flattened and linearly embedded into a vector.
- **Transformer Encoder Blocks**:
  - Multi-Head Self-Attention (MSA)
  - Layer Normalization + Residual Connections
  - Feedforward MLP (with GELU activation)
- Repeated for `L` blocks (L = number of encoder layers)

---

## Training Details

| Parameter            | Value                       |
|---------------------|-----------------------------|
| Model               | ViT-B/16                    |
| Epochs              | 20                          |
| Batch Size          | 32                          |
| Learning Rate       | 1e-4                        |
| Optimizer           | Adam                        |
| Loss Function       | CrossEntropyLoss            |
| Scheduler Options   | StepLR / Cosine + Warmup    |

### Learning Rate Schedulers

- **Cosine Annealing with Warmup**  
  Provides a smooth learning rate ramp-up followed by gradual decay. Helps stability during early training and improves generalization.

- **StepLR**  
  Drops learning rate sharply after fixed intervals. Simpler, but can lead to less stable training.

---

## Results

- Cosine + Warmup led to **smoother convergence** and better generalization than StepLR.
- ViT successfully classified Alzheimer’s stages from MRI scans, even for **underrepresented classes**.
- Demonstrated a significant improvement in minority class accuracy.

---

## Conclusion

The use of **Vision Transformers**, particularly with **Cosine Annealing and Warmup**, enhances classification performance in the domain of medical imaging. This project provides a step forward in developing AI tools to assist in early Alzheimer's diagnosis, potentially leading to **timely intervention and improved patient outcomes**.

---

## Authors

- **Giresh Aditya R**
- **Nandhini G** 
- **Rajasree S**

 May 2025

---

> 📌 *For medical use cases, consult with clinical professionals before deployment. This is a research project.*

