---
date: 2021-08-26
title: "[AI Boostcamp Day 18] Training and Inference"
categories: 
 - Naver AI Boostcamp Diary
tags:
 - P Stage
 - AI Stages
 - Deep Learning
 - Training and Inference

author: Hyeong
description: About Training and Inference of DL
---
### Training and Inference
- Blocks for Training
    - Loss
        - Loss function == Error function -> Used for backpropagation
        - Family member of nn.Module (actually)
            - This is why a single line of loss.backward() can cause back propagation
        - Focal Loss: for imbalanced dataset
        - Label Smoothing Loss
            - x one hot, smoother value
            - because objects or features of objects from other classes can coexist
    - optimizer
        - what updates the loss
        - StepLR (smaller every epoch)
    - Metric
        - Classification: Accuracy, F1-score, precision, recall, ROC&AUC
        - Regression: MAE, MSE
        - Balanced Data: Accuarcy ok
        - Imblanaced Data: F1-Score

- Training Process
    - model.train(mode=True)
        - set the module in training mode (loss change yes?)
    - optimizer.zero_grad()
    - criterion = torch.nn.SomeLoss()
    - loss = criterion(outputs, labels)
    - optimizer.step()
        - updates the gradient through the backward process
        - could use this function to incorporate smaller batches into larger batches
        ```python
        for i, data in enumerate(train_loader, 0):
            ...
            if i % NUM == 0:
                optimizer.step()
                optimzer.zero_grad()
        ```
- Inference Process
    - model.eval() (dropout, batchNorm off)
    - gradient should not be updated
    ```python
    with torch.no_grad():
        for data in dataloder:
    ```

### (Peer Session)[https://www.notion.so/2021-08-26-881b6b3372de4616be3b19cebf5a4dbf]

### What did I Do Today
- Fixed Errors in Dataloader
- Distributed Data Labeling process
- Trained the Model on Mask Dataset
- (Tried) to fix the loss
- Read and read and read the DL template

### Reflections
- Finish the lectures before 12
- Sleep fast!

