---
date: 2021-08-18
title: "[Paper Review] ViT (Vision Transformer)"
categories: 
 - Paper Review
tags:
 - Transformers
 - Image Recognition
 - Deep Learning
author: Hyeong
description: Image Deep Learning with Transformer Paper Review
---
#### Objective Paper:
[AN IMAGE IS WORTH 16X16 WORDS:
TRANSFORMERS FOR IMAGE RECOGNITION AT SCALE](https://arxiv.org/pdf/2010.11929.pdf)

#### 0. Abstract
- Transformer model has limited uses in CV
- Findings: Transformer only model can perform very well in CV
    - Significantly less computational resources needeed
    - Comparable accuracy

#### 1. Introduction
- In the NLP domain, self-attention based transformers performed great. Pre-training a large text corpus and then fine-tuning the model on a task-specific dataset was very effective
- In the CV domain, various efforts were present, but still CNN based architectures were more effective
- Training the model on mid-sized dataset? just modest
- Training the model on large datasets? Can be even better than edge-cutting CNNs

#### 2. Preceding Works
- Naive application of self-attention models to CV: not effective. each pixels relating to every other pixel producing toom much input for the model
- Attention to Neighboring pixles: promising results
- Most similar work with ViT: extracting 2 x 2 patches to embed them and use the attention model, but ViT can handle medium-resoltuion as well


#### 3. Method
![imgur](https://i.imgur.com/WG8STi3.png)
- ViT aims to apply the original transformer model as much as possible
- Model Structure
    1. Linear Projection of Flattened Patches
    - Original Image: <img src="https://latex.codecogs.com/gif.latex?\mathbb{R}^{H*W*C}" title="\mathbb{R}^{H*W*C}" />
    - Single Patch Size: <img src="https://latex.codecogs.com/gif.latex?P^2" title="P^2" />
    - Image Resolution: HW
    - Number of Channels: C
    - Number of Patches (Input Sequence Length for the Transformer): N = <img src="https://latex.codecogs.com/gif.latex?HW/P^2" title="HW/P^2" /> 
    - Constant Latent Vector Size (Single Flattened Patch): D
    - Single Patch Before Flattening: <img src="https://latex.codecogs.com/gif.latex?X_p^{i}&space;\in&space;\mathbb{R}^{P^2*C},&space;(1\leq&space;i\leq&space;N)" title="X_p^{i} \in \mathbb{R}^{P^2*C}, (1\leq i\leq N)" />
    - Trainable Linear Projection (for each patch): <img src="https://latex.codecogs.com/gif.latex?E&space;\in&space;\mathbb{R}^{(P^2*C)*D}" title="E \in \mathbb{R}^{(P^2*C)*D}" />
    - Class Vector: <img src="https://latex.codecogs.com/gif.latex?X_{class}" title="X_{class}" /> = <img src="https://latex.codecogs.com/gif.latex?Z^{0}_{l},&space;(l=0,&space;0\leq&space;l\leq&space;L)" title="Z^{0}_{l}, (l=0, 0\leq l\leq L)" />
    - Patch Position: <img src="https://latex.codecogs.com/gif.latex?E_{pos}^{i}&space;\in&space;\mathbb{R}^{D}" title="E_{pos}^{i} \in \mathbb{R}^{D}" />
    - Input for Transformer Encoder: <img src="https://latex.codecogs.com/gif.latex?Z_0&space;=&space;[X_{class};X^{1}_{p}E;X^{2}_{p}E;X^{3}_{p}E;...X^{N}_{p}E;]&plus;E_{pos}" title="Z_0 = [X_{class};X^{1}_{p}E;X^{2}_{p}E;X^{3}_{p}E;...X^{N}_{p}E;]+E_{pos}" />
    2. Alternation of MLP and MSA Layer
    - Layernorm (LN) is applied before every MLP and MSA block
    - MSA Layer = <img src="https://latex.codecogs.com/gif.latex?Z_l^{'}&space;=&space;MSA(LN(Z_{l-1}))&plus;Z_{l-1}&space;(l&space;=&space;1,&space;...,&space;L)" title="Z_l^{'} = MSA(LN(Z_{l-1}))+Z_{l-1} (l = 1, ..., L)" />
    - MLP Layer = <img src="https://latex.codecogs.com/gif.latex?Z_l&space;=&space;MLP(LN(Z_{l}^{'}))&plus;Z_{l}^{'}&space;(l&space;=&space;1,&space;...,&space;L)" title="Z_l = MLP(LN(Z_{l}^{'}))+Z_{l}^{'} (l = 1, ..., L)" />
    3. Output Layer
    - <img src="https://latex.codecogs.com/gif.latex?y&space;=&space;LN(Z^0_L)" title="y = LN(Z^0_L)" />

#### 4. Experiments
- Comparison of Models and the Size of Dataset
    - ViT, ResNet, and Hybrid
    - ViT adopts the configuration of BERT
    - ViT model differs depending on the size of the patch. The smaller the patch, the more complicated the model is. Each sequence length is inversely proportional to the square of the patch size
    - ViT model hyperparameters: <br/>
    ![Imgur](https://i.imgur.com/1J2KmBj.png)
    - ResNet with Batch Normalization for improvment
- Comparison of Performance
![Imgur](https://i.imgur.com/yCiU8nx.png)
    - ViT-H/14 and 16: Huge ViT model with patch size of 14 and 16
    - Hybrid Model, state of art in image classfication aside from ImageNet 
    - Noisy Student: CNN model, state of art in image classfication for ImageNet
    - Result: Some ViT outperform other models still consuming significantly less training resource
- Data Size and Performance of Pre-Trained Models
![Imgur](https://i.imgur.com/ZJmFKkn.png)
    - The capacity of the large ViT models are fully utilized only for larger datasets (JFT-300M)
- Scaling of Computational Resources
![Imgur](https://i.imgur.com/3yGaf30.png)
    - ViT outperforms ResNet in terms of the computational power and  the accuracy trade off
    - The Hybrid model learns the task faster, but the computational; power and the accuracy trade off increases and ViT cathes up with larger computational resources






