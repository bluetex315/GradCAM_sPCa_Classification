# GradCAM_sPCa_Classification

## Overview
This project is about establishing the Gradient-weighted Class Activation Mapping (Grad-CAM) on a ResNet-18 or ResNet-34 model for significant vs non-significant prostate cancer classification task. There is only one file named `GradCAM_ResNet18_ISUPClassification_partialdata_binary_2d_nodp_nobn.ipynb`

## Features
- Implementation of Grad-CAM for detailed visual insights into model predictions.
- Custom adaptation of ResNet18 and ResNet34 tailored for medical image processing.

## Requirements
- Python 3.9
- monai 0.9.0
- PyTorch 1.11.0
- Matplotlib

## Dataset
The dataset being used can be requested at https://pi-cai.grand-challenge.org/
It consists of 1500 3D prostate MRI scans. Besides T2W and ADC images, the whole gland segmentation and lesion segmentation by AI and human annotation is also available for this challenge.

## Usage
Execute from the top to bottom cells of the Jupyter notebook to apply the model. It mainly composed of 4 parts:
1. Data loading and processing
This step loads in the dataframe for all meta-information including the path to images, ISUP values of the patients, and all other details.
```df_picai``` dataframe is the comprehensive dataframe, and ```df_picai_balanced``` is the dataframe that subsampled healthy scans in order to balance the number of positive and negative scans.

2. Image preprocessing
This step preprocesses the images, T2W, ADC, whole gland segmentation, and lesion segmentation before training the neural network. All the images were loaded by <<NibabelReader>> and cropped by foreground which is the whole gland segmentation. The images were set to be (3, 128, 128) where 3 represents number of channels, namely whole gland segmentation, ADC map, and T2W. And 128 was the number of height and width for the images. Image intensity is scaled by `monai.transforms.ScaleIntensityRangePercentilesd`.

3. ResNet Model
Two ResNet models were developed in this stage, ResNet-18 and ResNet-34, and they were built from scratch. Each model was trained on different settings (batch norm, dropout). The learning rate is set to 1e-5 with cosine annealing scheduler. Both models were trained on Quadro RTX 8000 with 300 epochs.

4. Building GradCAM and Inference
GradCAM was built from the 4-th layer of the ResNet Block, which is the last convolutional layer before global average pooling and fully connected network. For inference, the acquired heatmap was reshapped to the original size by bilinear interpolation. And it is overlaid on the T2W for visualization. For inference, test accuracy, precision, recall, and AUC were reported.
