# RSNA-breast-cancer deep learning radiomics

## Overview
This work implied testing of pretrained neuronal networks for radiographic breast image classification (heathy/cancer).

## Datasets
The RSNA breast cancer train dataset contains 11913 mammograms of healthy subjects and patients with breast cancer. A csv file with  metainformation (patients age, image view, image laterality etc.) is available. The dataset can be upload from the Kaggle repository [https://www.kaggle.com/competitions/rsna-breast-cancer-detection/data].

## Code
### rsna-breast-cancer-pt-1-exploratory-data-analysis.ipynb
On the first step exploratory analysis of metadata was performed to gain better understanding of the overall dataset. 
On the second step mammograms from various patient groups (e.g. healthy subjects, cancer patients, subjects with breast implants) were visualized.
### rsna-breast-cancer-pt-2-image-processing.ipynb
Based on the results from the previous steps following preprocessing steps were done:
1. The dataset weights >300 Gb and 11913 images but it's very unbalanced as only 4% of images were derived from cancer patients. We therefore reduced number of images derived from healthy patients.
2. The images have different properties (photometric interpretation, size), contain a lot of empty space and artefacts, so regions of interest were selected, figures were standartized, cropped and saved in a png format. 

### rsna-breast-cancer-pt-3-model-training
We split the dataset into training and validation parts at a ratio of 3 to 1. We used data augmentation to increase number of observations for cancer patients and make parameter estimation more stable. 
On the first step we tested several pretrained models (resnet50, alexnet, vgg11, vgg16, vgg19, squeezenet, densenet) and selected the one based on the validation metrices. The best result was observed for VGG models and vgg11 was selected for further work.
We then used vgg11 as a feature extractor and combined it with classificator exploiting csv metadata which enabled us to improve performance of the model.
On the next step we tried to further improve model performance via unfreezing of fully connected layers but this led the overfitting problem, so, unfreezed models were not used.
### rsna-breast-cancer-pt-4-inference
The best model was used for prediction of cancer probability based on test images and csv metadata.
