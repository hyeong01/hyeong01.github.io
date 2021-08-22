---
date: 2021-08-19
title: "Tensorboard Short Note"
categories: 
 - Deep Learning Visualization
tags:
 - Deep Learning
 - Tensorboard
 - Visualization
author: Hyeong
description: Tensorboard Short Note
---

### Tensorboard
- Supports PyTorch
- Shows scalars (accuracy, loss etc)
- Shows the computational graph
- Shows the histogram of weights

1. How to Use
- Create directory to save log
```python
import os
log_dir = 'log_file'
os.makedirs(log_dir)
```
- Import tensorboard log writer
```python
from torch.utils.tensorboard import SummaryWriter
import numpy as np
```

```python
- create different experiments
experiment_dir = log_dir + '/exp1'
writer = SummaryWriter(experiment_dir)
```

- Log content
```python
for iter_nth in range(100):
    writer.add_scalar('loss/train' value, iter_nth)
writer.flush() # save log on the drive
```
- Activate Tensorboard on Jupyter Notebook
```python
%load_ext tensorboard
%tensorboard --logdir {log_dir}
```
