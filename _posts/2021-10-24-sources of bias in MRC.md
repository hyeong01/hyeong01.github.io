---
date: 2021-10-24
title: "Source of Bias in MRC"
categories: 
 - MRC
tags:
 - MRC
 - Boostcamp
author: Hyeong
description: Summary of Lectures
---
## 1. Mitigating Training Bias
- A lot of bias present; models can learn sexual bias 

#### a. Traing Bias in Reader Model
- Reader models are prone to train only on a limited designated number of documents
- If the reader model is given a text from a relatively new subject, the reader model will have hard time producing the answer
- Solution:
    - For the reader model: by enabling the model to provide a "no answer", we can train the model on larger sets of documents with no answer
    - For the retriever model: train the DPR with negative samples with high BM25 scores

## 2. Annotation Bias from Datasets
- If the dataset creator already knows the answer of a question, then the question can have too much hints, making the retrieval task too simple
- We can adopt natural questions that real users have produced on the internet to avoid such bias
- Ground truth might not include all possible answers, penalizing the model that actually produced a correct answer

