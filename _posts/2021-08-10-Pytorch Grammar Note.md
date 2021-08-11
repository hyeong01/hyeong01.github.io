---
date: 2021-08-11
title: "Pytorch Grammar Note"
categories: 
 - Pytorch
tags:
 - Deep Learning
 - Pytorch
 - Python
author: Hyeong
description: Pytorch Grammar Note
---
## Numpy to Tensor
__torch.tensor(arg) vs torch.from_numpy(arg)__
- both generate a tensor, but only torch.from_numpy(arg) shares the memory with original numpy array


