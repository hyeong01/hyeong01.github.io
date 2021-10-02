---
date: 2021-08-20
title: "[AI Boostcamp Day 14] All about the Training Process"
categories: 
 - Naver AI Boostcamp Diary
tags:
 - Multi-GPU training
 - Hyperparameter Tuning
 - PyTorch Trouble Shooting
 
author: Hyeong
description: all about training
---

### What I studied today:
1. Multi-GPU Training
- Huge Data -> need of powerful hardware
- GPU vs Node
    - GPU is a card
    - Node is a computer
    - Multi Node Multi GPU: collection of fucking awesome computing machines
- Parallel
    - Model Parallel
        - Not Popular. Hard
    - Data Parallel
        - e.g. independently computing the loss and averaging it to compute the gradient
        - simple data parallel is very easy
        ```python
        # just have to add a single code!
        model = torch.nn.DataParallel(Model)
        ```
        - Disbtributed data parallel is a bit more complicated (needs multiprocessing)

2. Hyperparameter Tuning
- finding the learning rate, epoch etc.
- Recently small room for improvement with hyperparameter tuning
- Grid vs Random
    - ![imgur](https://i.imgur.com/pH0qRsw.png)
    - grid: via designated space
    - random: random literally
- Ray
    - Standard multi-node multi processing module for ML and DL
    - Numerous module for hyperparameter search
    - the whole training process should be in a single function to use ray

3. PyTorch Trobuleshooting
- OOM (Out of Memory)
    - Hard to know why and where it occurred 
    - How to solve? smaller batch size!
- Dealing with the problem in GPU 
    - checking if the RAM is leaking; check if the RAM usage is increasing at each iteration
    ```python
    from GPUtil import showUtilization
    showUtilization()
    ```
    - deleting  the tensors and emptying the cache to secure needed RAM
    ```python
    del tensorList
    torch.cuda.empty_cache()
    ```
    - tensor variables accumulate. 
    - change to python basic variable to prevent the accumulation
    - variables inside the loop still exist after the loop
    - torch.no_grad()
        - during no_grad status, no backward pass -> less use of memory
- Most of the errors from CNN are from the mistach of size
- can change the precision of tensor to 16bit
