---
date: 2021-08-19
title: "Basic Weight and Biases with Code"
categories: 
 - Deep Learning Visualization
tags:
 - Deep Learning
 - Weight and Biases
 - Visualization
author: Hyeong
description: Weight and Biases Basics
---

### Weight and Biases
- Easy to share the experiemnt with other people!
- can track hardware status
- install with pip
```python
!pip install wandb -q
```
- make config file
```python
config={"epochs":EPOCHS, "batch_size":BATCH_SIZE, "learning_rate":LEARNING_RATE}

# initialize! set entity name from web
wandb.init(project="project_name", entity="entity_name")

# after setting the configuartion dictionary
wandb.init(project="project_name", config=config)

# setting configuration 
wandb.config.batch_size = BATCH_SIZE
wandb.config.learning_rate = LEARNING_RATE
```
- how to use in the model
```python
for e in range(1, EPOCHS+1):
    epoch_loss = 0
    epoch_acc = 0
    for X_batch, y_batch in train_dataset:
        X_batch, y_batch = X_batch.to(device), y_batch.to(device).type(torch.cuda.FloatTensor)
        ...

        ...
    # saving the log
    wandb.log({'accuary':train_acc, 'loss':train_loss})
```

