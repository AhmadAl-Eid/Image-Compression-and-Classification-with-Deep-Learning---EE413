# Image-Compression-and-Classification-with-Deep-Learning---EE413

Image Compression and Classification using Mini-ImageNet Dataset

EE 413: Applied Digital Signal Processing Spring 2026 (252)

King Fahd University of Petroleum and Minerals (KFUPM)  
Department of Electrical Engineering

This project study the effect of image compression on image classification. Two pre-trained models ResNet18 and MobileNetV3-Small are fine-tuned on the Mini-ImageNet dataset. After establishing baseline performance on uncompressed images wavelet image compression is applied at different compression ratios and the change in classification accuracy is analyzed.

# Methodology

## Model Selection and Baseline Establishment - Ahmad Al-Eid
### 1. Dataset Preparation

Mini-ImageNet dataset with 100 classes

Images resized to 96 × 96 pixels

Training and validation split

ImageNet normalization applied for pre-trained models

### 2. Model Selection and Baseline Establishment

Two models selected:

ResNet18

MobileNetV3-Small

Both models were fine-tuned on the original Mini-ImageNet training set

Baseline performance was evaluated on the uncompressed test set

### 3. Training Setup

Loss function: CrossEntropyLoss

Optimizer: AdamW

Batch size: 64

Maximum epochs: 8

Learning rate for ResNet18: 0.0003

Learning rate for MobileNetV3-Small: 0.0004

Weight decay: 0.0001

Early stopping patience: 3 epochs

### 4. Validation Strategy

Training and validation accuracy were tracked across epochs

Validation results were used to check generalization and reduce overfitting

Early stopping was applied when validation performance stopped improving

<img width="1389" height="490" alt="image" src="https://github.com/user-attachments/assets/270d0f7c-2e93-4e27-820e-df93ba74f38f" />


### 5. Baseline Results

ResNet18 achieved the best baseline performance on uncompressed test images

ResNet18 test accuracy: 74.7%

MobileNetV3-Small test accuracy: 72.6%

ResNet18 also achieved higher macro-F1 and lower test loss

tradeoff:

ResNet18 higher accuracy but MobileNetV3-Small gives better efficiency and smaller model size

| Model | Parameters | Best Validation Accuracy | Test Loss | Test Accuracy | Test Macro-F1 |
|---|---:|---:|---:|---:|---:|
| ResNet18 | 11.21M | 0.756 | 0.987 | 0.747 | 0.747 |
| MobileNetV3-Small | 1.58M | 0.725 | 1.117 | 0.726 | 0.725 |



## Wavelet-Based Image Compression

Mohammed alduabis

## Training on Compressed Data

Ali Alhaji - Faisl Alsalhi


# Team Members

Ahmad Al-Eid

Ali Alhajji

Mohammed Aldubais

Faisal Alsalhi

# Libraries Used

The required Python packages are listed in `requirements.txt`

Python

PyTorch

Torchvision

NumPy

Matplotlib

Scikit-learn

PyWavelets

Pandas
# How to install the dataset before running the project

1. Go to google drive then my drive and upload folder and name it EE413 then create another folder inside it and name it miniimagenet and upload the trian,val,test files

# Setup Instruction

To run this project, clone the repository and install the required Python libraries from `requirements.txt`.

```bash
git clone https://github.com/AhmadAl-Eid/Image-Compression-and-Classification-with-Deep-Learning---EE413.git
cd "2nd project-Final"
pip install -r requirements.txt





# What Fine-tuning Model Two does 

| Step | Description |
|------|-------------|
| 1 | Defines `wavelet_compress()` — applies 2-level Haar DWT + hard thresholding |
| 2 | Wraps the training set in `CompressedDataset` (threshold = 0.15, ~5:1 ratio) |
| 3 | Deep-copies `mobile_pulse` so the original baseline stays intact |
| 4 | Fine-tunes the copy for 5 epochs with early stopping (patience = 3) |
| 5 | Saves the fine-tuned model to Google Drive |
| 6 | Evaluates both models on the test set at all 3 compression levels |
| 7 | Produces comparison tables, line plots, and a robustness heatmap |




| File | Description |
|------|-------------|
| `mobilenet_compressed_ft.pth` | Fine-tuned model weights |
| `training_history.csv` | Loss and accuracy per epoch |
| `comparison_results.csv` | Accuracy and F1 for both models × all compression levels |
| `accuracy_drop.csv` | How much each model degrades under compression |
| `training_curves.png` | Loss curve + accuracy per epoch plot |
| `comparison_plot.png` | Accuracy and F1 vs compression level (line chart) |
| `drop_heatmap.png` | Accuracy drop heatmap (green = robust, red = sensitive) |

---

## Results Summary

### Training (MobileNetV3-Small on Compressed Data)

| Epoch | Train Loss | Train Acc | Val Acc | LR |
|-------|------------|-----------|---------|-----|
| 1 | 0.4193 | 0.8709 | 0.7169 | 5e-5 |
| 2 | 0.3702 | 0.8834 | 0.7177 | 5e-5 |
| 3 | 0.3353 | 0.8971 | **0.7219** | 5e-5 |
| 4 | 0.3080 | 0.9052 | 0.7174 | 5e-5 |
| 5 | 0.2882 | 0.9094 | 0.7195 | 2.5e-5 |

Best validation accuracy: **72.19%** at Epoch 3.

---

### Performance Comparison — Original vs Fine-tuned

| Model | Compression | Accuracy | Macro F1 |
|-------|-------------|----------|----------|
| MobileNetV3 (Original) | None (Baseline) | 0.7010 | 0.6999 |
| MobileNetV3 (Original) | Low (2:1) | 0.7023 | 0.7017 |
| MobileNetV3 (Original) | Medium (5:1) | 0.6854 | 0.6864 |
| MobileNetV3 (Original) | High (10:1) | 0.5997 | 0.6014 |
| MobileNetV3 (Compressed FT) | None (Baseline) | 0.7234 | 0.7221 |
| MobileNetV3 (Compressed FT) | Low (2:1) | 0.7255 | 0.7243 |
| MobileNetV3 (Compressed FT) | Medium (5:1) | 0.7214 | 0.7214 |
| MobileNetV3 (Compressed FT) | High (10:1) | **0.6781** | **0.6799** |

---

### Robustness — Accuracy Drop vs Each Model's Baseline

| Model | Compression | Drop |
|-------|-------------|------|
| Original | Low (2:1) | -0.001 |
| Original | Medium (5:1) | 0.016 |
| Original | High (10:1) | **0.101** |
| Compressed FT | Low (2:1) | -0.002 |
| Compressed FT | Medium (5:1) | **0.002** |
| Compressed FT | High (10:1) | **0.045** |

> Negative drop = accuracy gain over baseline. Positive drop = accuracy loss.

---

### Key Takeaways

- Fine-tuned model has **55% less accuracy drop** at High (10:1) compression — 0.045 vs 0.101
- **10× less degradation** at Medium (5:1) compression — 0.002 vs 0.016
- Fine-tuned model outperforms the original at **all compression levels**, including on clean uncompressed images (+2.4%)
- Training on compressed data teaches the model to rely on low-frequency wavelet features that survive compression, making it more robust overall
