---
date: 2021-08-18
title: "AI Boostcamp Day 12"
categories: 
 - AI Boostcamp
tags:
 - AutoGrad
 - Optimizer
 - Dataset
 - Dataloader
author: Hyeong
description: Basic Pytorch Implementation
---

### What I studied today:
1. AutoGrad & Optimizer
- nn.Parameter
    - Inherits tensor object
    - If an attribute of nn.Module, required_grad = True
    - Usually inside the layers (not usually delcared independently)
- Backward Process from the Scratch
    - optimizer automatically does the job
    - Can get deriviative manually
2. Dataset & DataLoader
- ToTensor(): to numerical format
- transforms: preprocessing
- Dataset: object that decides how to load a single data
- DataLoader: providing data to the model via batch, suffle etc.

3. [ViT Paper Review](https://hyeong01.github.io/paper%20review/Transformers-for-Image-Recongnition-at-Scale/)



