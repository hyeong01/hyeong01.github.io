---
date: 2021-08-24
title: "[AI Boostcamp Day 16] Dataset and Data Generation "
categories: 
 - AI Boostcamp
tags:
 - P Stage
 - AI Stages
 - Data Generation

author: Hyeong
description: About Dataset 
---
### What I Learned Today
1. Pre-processing
    - 80% time of the project   
    - Image Dataset
        - bounding box: sometimes to remove noise

2. Generalization of Dataset
    - Underfitting (High Bias) vs Good vs Overfitting (High Variance)
    - Train / Validation
        - Why need validation set?: to validate the training process. The model is already trained with the train set so need a seperate set to check if the model is heading to a right direction
    - Data Augmentation
        - Diversity of cases and states
        - torchvision.transforms.Compose([ ... ])
        - Albumentations (faster and more diverse than the torch library)
    - Importance of experiemnt: there is almost no technique that always enhancese the performance. Always try and validate

3. Data Generation
    - CPU bottleneck (slow feeding speed)  
    - e.g. data augumentation
    - Dataset defining code
    ```python
    from torch.utils.data import Dataset
    
    class MyData(Dataset):
        def __init__(self):
            pass
        
        # support slicing
        def __getitem__(self,index):
            return index
        
        # support len()
        def __len__(self):
            return None
    ```
    - Dataloader code
    ```python
    from torch.utils.data import DataLoader
    loader = DataLoader(
        train_set,
        batch_size=bs,
        num_workers=num,
        drop_last=True
    )
    ```





### 오늘 할일
- [x]  강의 및 강의 노트
- [ ]  스페셜 미션 ㄱㄱ
- [ ]  데이터 EDA (아마 못할 듯)

### [오늘 피어 세션](https://www.notion.so/aa5b217b9b0140cfb10f4ec980b36c87?v=790a78942a234318a9bd84c5d5acfa4b&p=4d7097c0d2144eecabbf429c3e94fa2e)
