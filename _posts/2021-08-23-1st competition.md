---
date: 2021-08-23
title: Boostcamp First CV Competition Abstract
categories: 
 - Competition
tags:
 - P Stage
 - AI Stages
 - Deep Learning
 - CV
 
author: Hyeong
description: First boostcamp CV competition
---
### Goal
- Classify 18 agumented classes
    - 3 age intervals
    - mask, no mask, and incorrect mask
    - male or female

### Objective
- Learning how to enhance DL model
- Learning a part of DL pipeline

### Data Description
- Metadata Field, file format

### Discussion
- Way to improving together

### Answer Submission
- File name and answer label in csv
- How to create the answer label file?
    - With python IDLE (the hosts will provide it)
    - Jupyter Notebook

### Questions
- Many data fields.. aside from the image itself. how can I use it? -> The goal is to predict all labels

### Ideas
- (Done) The faces in the photo are always in the middle. We can crop it for better performance
- (Failed due to too much time) Better to have the result for each classes from different models or at least from a different vector. The suggested class of 0 from 17 with different classes merged into one vector is undesirable 
- (Works Great) Stratified Dataset according to personals. Same person, many photo -> could be in both the train and test dataset -> could make the validation set less meaningful
- (Fun, easy to share) Transformation Cafe. Sharing sorts of transformations as cafe menus
- (Stupid that we weren't doing it) Validation and train set split
- (Seemingly useful for now) learning rate scheduler -> CosineAnnealingLR
- (Great) Tidying up is so important. Name the model weights and tensorboard running log with time and other recognizable variables
- (Trying out) Shouldn't the transformation on validation be the same one with the one on test data?
- (Very Useful) Any errors from the dataset or data loader? Any wrong labels from the first place? -> YES

### Techniques
- Imbalanced dataset problem
    - Use focal loss
    - Use data augumentation
- Resize
    - original size of dataset 500x384
    - 400x384 -> no face crop
    - 384x384 -> very little face crop, still decent
- Model Form 
    - destination class: 3 X
    - 3 heads 1 model X
    - 1 head 3 models X
    - For debugging and fast training purposes -> 1 model 1 head!

### (Model Tryouts)[https://www.notion.so/Parameter-7c91e3d70ec2404a9e56a49e78806d33]
