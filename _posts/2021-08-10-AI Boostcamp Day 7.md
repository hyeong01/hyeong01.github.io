---
date: 2021-08-09
title: "AI Boostcamp Day 7"
categories: 
 - AI Boostcamp
tags:
 - Pytorch
 - Optimization
 - Python
author: Hyeong
description: Neural Network Optimization
summary: 123
---

#### What Constitutes an Optimization
1. Generalization: Training the network with a train data to perform well on an actual data.
- Generalization Gap: the difference of the performance of the model on the train data and the actual data.
2. Cross-validation: iterating through the training dataset and using it as a validation data. Often used when finding a hyperparameter.
3. Bootstrapping: Random sampling with replacement and creating multiple models to train or test the model.
4. Bagging: Training multiple models with boostrapping and accumulating the models through measures such as voting or averaging.
5. [Boosting](https://hyeong01.github.io/math/Boosting-Basic-Concepts/)
6. Gradient Descent Methods
- Stochastic Gradient Descent: Traing the model with a single sample, one by one.
- Mini-batch Gradient Descent: Training the model with a subset of data.
- Batch Gradient Descent: Updating the gradient with the whole dataset.
- Batch-size Matters!: "large batch methods tend to converge to sharp minimizers ... small-batch methods consistently converge to flat minimizers<sup>1)</sup>"
- ![Imgur](https://i.imgur.com/jp057q9.png)
7. Gradient Descent Functions
- Basic Gradient Descent
- Momentum
- Nesterov Accelerate
- Adagrad
- RMSprop
- Adam
8. Regularization: limiting the training procedure so that the model also performs well on other datasets (preventing overfitting)
- Early stopping: stopping when the validation error is at its minimum
- Parameter Norm Penalty: smoothening the functional form of the neural model by limiting the size of the weight
- Data Augmentation: neural model tends to need significantly more data to train. DA is modifying the data to enlarge the dataset
- Label Smoothing: constitutes of mixing inputs (by collaging images) and answer labels (by giving decimal numbers as answer labels). Alleged to smooth the decision boundary.
- Dropout: excluding random neurons at every foward propagation
- Batch Normalization: computing sample mean and variance and normalizing each batch. No definite answer on why this increases the performance of the model. Variance of BN includes layer normalization, instance normalization, and group normalization

*Reference:* <br/>
1) Keskar, Nitish. *On Large-Batch Training for Deeping Learning: Generalization Gap and Sharp Minima* 20160915

