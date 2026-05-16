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
