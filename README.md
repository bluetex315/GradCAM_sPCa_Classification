# GradCAM_sPCa_Classification

## Overview
This project is about establishing the Gradient-weighted Class Activation Mapping (Grad-CAM) on a ResNet-18 or ResNet-34 model for significant vs non-significant prostate cancer classification task. There is only one file named `GradCAM_ResNet18_ISUPClassification_partialdata_binary_2d_nodp_nobn.ipynb"

## Features
- Implementation of Grad-CAM for detailed visual insights into model predictions.
- Custom adaptation of ResNet18 tailored for medical image processing.

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
After getting the ```df_picai```

3. Image preprocessing

4. ResNet Model

5. Building GradCAM and Inference
