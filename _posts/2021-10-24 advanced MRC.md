---
date: 2021-10-24
title: "Advanced Topis in MRC"
categories: 
 - MRC
tags:
 - MRC
 - Boostcamp
author: Hyeong
description: Summary of Lectures
---
## 1. Closed-book QA
- Popular approaches such as MRC and Open-domain QA are allowed to use supporting documents outside of the model
- New approaches have tried to save the information in the model parameters
#### a. Text-to-Text Format
- Similar to Gerative MRC, except that the model is not provided with contexts
- Uses seq-to-seq transformer models like BART, and the input consists of a question and the explanation of the task
    - example of an input: "translate English to German: I love this"
- T5 Model:
    - Seq-to-Seq transfomer model that can perform universal NLP tasks
    - Profound fine-tuning, model, and data for pretraining experiment
    - All info stored on model -> huge parameter size

## 2. QA with Phrase Retrieval
- An experiment to get an answer directly without the retrieval process
- Takeaway: Use both the dense encoding and spare encoding since they are different focus. Sparse encoding focuses more on the vocab and the dense encoding focus more on the meaning.

