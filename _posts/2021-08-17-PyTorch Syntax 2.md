---
date: 2021-08-17
title: "PyTorch Syntax 2"
categories: 
 - PyTorch Syntax
tags:
 - Deep Learning
 - Pytorch
 - Python
author: Hyeong
description: Basic Pytorch Implementation
---
#### Pytorch Tensor perators
    - Numpy + AutoGrad
    - Tensor
        - list (Python) -> Ndarray (Numpy) -> Tensor (PyTorch)
        - Almost identical with Ndarray
        - Shares similar grammars with Numpy array
        - Can produce from list or Ndarray 
        - Tensor operations can utilize GPU unlike Numpy
        - Use view instead of reshape function. Reshape creates a copy of the original tensor, whereas view only create a copy that is presented in a designated shape
        - mm vs matmul: the same, but matmul supports boradcasting, thus could be confusing
        <br/>        
        - Examples:
        
```
import numpy as np
import torch

# creating tensors
>>> py_list = [[1,2],[3,4]]
>>> nd_array = np.array(lst)
>>> torch.tensor(py_list)
tensor([[1,2],[3,4]])
>>> torch_tensor = torch.tensor(nd_array)
>>> torch_tensor
tensor([[1,2],[3,4]])

# similar grammars with Numpy
>>> torch_tensor.ndim
2
>>> torch_tensor.shape
torch.Size([2,2])
>>> torch_tensor[0]
tensor([1,2])

# Utilizing GPU
>>> torch_tensor.device
# computation will be done on CPU for this tensor
device(type='cpu')
# check if GPU is available
>>> torch.cuda.is_available()
True
# computation will be done on GPU for this tensor
>>> torch_tensor_cuda = torch_tensor.to('cuda') 
>>> torch_tensor_cuda.device
device(type='cuda', index=0)

# Squeeze
>>> t_tensor = torch.rand(size=(2,1,2,1))
tensor([[[[0.3512],
          [0.4691]]],
        [[[0.8386],
          [0.1982]]]])
>>> t_tensor.squeeze().shape()
torch.Size([2,2])
>>> t_tensor.unsqueeze(0).shape()
torch.Size([1,2,2])
```




