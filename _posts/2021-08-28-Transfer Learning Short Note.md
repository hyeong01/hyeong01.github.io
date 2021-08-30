---
date: 2021-08-19
title: "Transfer Learning Tips"
categories: 
 - Transfer Learning
tags:
 - Deep Learning
 - PyTorch
 - Tranfer Learning
author: Hyeong
description: Transfer Learing Tips
---

### Transfer Learning Tips
- About the LR
    - When not freezing the backbone and when the new fully connected layers are initialized, the learning rate should be small. The FCs are significantly out of shape, and the loss could ruin the backbone if the learning rate is big.
- Training Sequence
    - Thus, it is best to freeze the backbone model until FCs settle with medicore weights, if not best. 