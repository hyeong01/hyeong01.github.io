---
date: 2021-08-09
title: "AI Boostcamp Day 6"
categories: 
 - AI Boostcamp
tags:
 - Pytorch
 - MLP
 - Python
author: Hyeong
description: Basic Pytorch Implementation
---

### What I studied today:
#### History of Deep Learning
1. AlexNet (2012): first to prove the performance of neural networks. Outperformed conventional statistical machine learning methods for the first time in an image classification task.
2. DQN (2013): advent of reinforcement learning, e.g. AlphaGo
3. Encoder / Decoder (2014): proved that Encoder-Decoder structure can outperform the RNN structure.
4. Adam Optimizer (2014): the rule-of-thumb optimizer for deep learning. Decent performance most of the time.
5. GAN (2015): neural networks can now generate images.
6. Residual Networks (2015): deeper implementations of neural networks possible. Partial solution to the vanishing gradient problem.
7. Transformer (2017): ???
8. BERT (2018): ???
9. Self Supervised Learning: adoption of non-labeled data in the training process.<br/><br/>

#### Multi-layer Perceptron
1.  Loss Functions: 
* Regression Task > MSE <br/>
&nbsp; - Why MSE?: MSE is an equative process of MLE on a linear Gaussian model. 
* Classification Task > CE <br/>
&nbsp; - Equation: <img src="https://latex.codecogs.com/svg.latex?-\sum_{c=1}^{C}y_clog(\widehat{y_c})" title="-\sum_{c=1}^{C}y_clog(\widehat{y_c})" /> <br/>
&nbsp; - Explanation: <img src="https://latex.codecogs.com/svg.latex?y_c" title="y_c" /> is an element of an one hot encoded vector. The higher the uncertainty is (or the lower the probablity is), the larger the absolute value of <img src="https://latex.codecogs.com/svg.latex?log(\widehat{y_c})" title="log(\widehat{y_c})" /> is. Simply put, the loss falls if the model can predict the correct label with a higher probablilty. 
* Probablistic Task > MLE


*Reference:* 
1. Britz, Denny. *Deep Learning's Most Important Ideas - A Brief Historical Review*. 2020-07-29

