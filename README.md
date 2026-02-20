# Deep Learning for Knee MRI Reconstruction

This project implements a **UNet-based Convolutional Neural Network (CNN)** to reconstruct high-fidelity MRI images from highly undersampled k-space data. Using the **fastMRI** dataset, the model addresses the challenge of accelerating MRI acquisition times by reconstructing full images from only **25% of the raw data**.

## Key Results
| Metric | Result | Note |
|:-------|:-------|:-----|
| **PSNR** | **24.15 dB** | Peak Signal-to-Noise Ratio on Test Set |
| **SSIM** | **0.7884** | Structural Similarity Index Measure |
| **Acceleration** | **4x (25%)** | Retained data vs. full k-space |

## Methodology
### 1. Architecture
* **Backbone:** Custom UNet implementation with encoder-decoder paths and skip connections to preserve high-frequency details.
* **Input:** Complex-valued k-space data (converted to 2-channel tensors).
* **Optimization:** Utilized **L1 Loss** (Mean Absolute Error) instead of MSE to mitigate blurring and preserve edge sharpness.

### 2. Data Processing
* **Dataset:** [NYU fastMRI Knee Dataset](https://fastmri.med.nyu.edu/)
* **Preprocessing:** Applied random masking to simulate 4x acceleration (25% sampling).
* **Multi-Coil Integration:** Implemented Root-Sum-of-Squares (RSS) reconstruction to combine data from multiple receiver coils.

## Installation
```bash
pip install -r requirements.txt
python train.py --epochs 50 --batch_size 16
