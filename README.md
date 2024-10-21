# Ovarian Cancer Subtype Classification

## Overview

This project focuses on classifying subtypes of ovarian cancer using Whole Slide Images (WSI) and Tissue Microarrays (TMA) data from the [UBC-OCEAN Kaggle competition](https://www.kaggle.com/competitions/UBC-OCEAN). The task is to classify ovarian cancer images into the following subtypes:

- **Clear Cell Carcinoma (CC)**
- **Endometrioid Carcinoma (EC)**
- **High-grade Serous Carcinoma (HGSC)**
- **Low-grade Serous Carcinoma (LGSC)**
- **Mucinous Carcinoma (MC)**
- **Other** (Note: This class is absent in the training set but present in the test set.)

The dataset consists of images from different hospitals, with the test set containing images from institutions not represented in the training set, adding a challenge of domain shift.

<img width="1520" alt="OCEAN-Optional-Figure" src="https://github.com/user-attachments/assets/95c01abd-6f40-4f13-bdea-1cddcdfb7199">

## Data Description

- **WSI (Whole Slide Images):** Large images (up to 100,000 x 50,000 pixels) at 20x magnification. The average file size is 1-2 GB.
- **TMA (Tissue Microarrays):** Smaller images (~4,000 x 4,000 pixels) at 40x magnification, but there are relatively fewer TMA samples in the dataset.

## Methods and Experiments

### TMA Experiments

Due to the limited number of TMA images, several approaches were explored:

- **Data Augmentation:** Various augmentation methods were applied to increase the amount of training data, including rotations, flips, and color transformations.
- **Cross-Validation:** Cross-validation was employed to improve model generalization.
- **Feature Clustering:** Features were extracted from the images and then clustered to explore patterns and improve classification accuracy.
- **Tiling:** TMA images were divided into smaller tiles, and tile-wise predictions were aggregated to classify the entire image based on the most common tile prediction.
- **Autoencoder:** An autoencoder trained on external TMA images from different cancers (scraped from Stanford's Tissue Microarray database) was used for feature extraction.
- **Segmentation and Core Detection:** Segmentation algorithms were used to detect the tissue cores within the TMA images.

**Results:** 
The classification results for TMA images were less promising, likely due to the small dataset size and lack of variation.

### WSI Experiments

Given the enormous size of WSI images, the following techniques were applied:

- **Multiple Instance Learning (MIL):** MIL classifiers were used where each WSI image was treated as a bag of feature vectors. The model was tasked with learning from these instances without requiring precise region annotations.
- **Tiling and Feature Extraction:** Similar to TMA, WSI images were divided into smaller tiles. Feature extraction was performed on these tiles using pre-trained models like ResNet.
- **Clustering:** Features extracted from WSI tiles were clustered, and the cluster information was used as additional input for model training, improving the model's ability to differentiate between cancer subtypes.
- **Hyperparameter Tuning:** Various hyperparameters were tuned across different experiments to optimize model performance, which is detailed in the corresponding Jupyter notebooks.

**Best Approach:** 
The MIL classifier approach, treating WSI images as bags of instances, yielded the best performance.

## Results
### TMA Experiments:
Results were less successful due to the small dataset and lack of class variation. The best approach involved data augmentation and tiling, but performance was still limited.

### WSI Experiments:
The best performing model was the MIL classifier, which treated each WSI as a collection of feature vectors. Additional improvements were achieved through feature clustering and hyperparameter tuning.

