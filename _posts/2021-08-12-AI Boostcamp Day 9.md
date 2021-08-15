---
date: 2021-08-12
title: "AI Boostcamp Day 9"
categories: 
 - AI Boostcamp
tags:
 - RNN
 - Machine Learning
 - Deep Learning
author: Hyeong
description: Basic Pytorch Implementation
---

### What I studied today:
1. Sequential Model:
- Problem: does not know about the dimension of the input
- Naive Sequence Model:
    - Consider all information from the past. Problem: how many?
- Autoregressive Model:
    - Fix time frame
- Markove Model:
    - First-order autoregressive model
- Latent Autoregressive Model:
    - Hidden state includes summarizes the past information and the output considers only one hidden state
- Recurrent Neural Network:
    - Drawback: Shorterm dependencies. Information from long ago fades
    - Hidden state goes through multiple layers to reach other layers -> vanishing / exploding gradient
    - "image"
- LSTM:
    - Devised to prevent the shorterm dependemncy problem of RNN
- GRU:
    - No cell state unlike LSTM
    - Hidden state itself is an output
    - Less parameter than LSTM -> better performance than LSTM
2. Tramsformer:
    - To solve the problem in dealing with sequential data; the input often changes in sequence and length
    - recursive x attententive o
    - "Image"
    - Encoder (attention)
        - Not regressive
        - Create query vector, key vector, and value vector for each word
        - Dot product the query and key vector
        - Regularize it with the root dimension of key vector and use softmax
        - the weighted sum of value vectors is the output from the encoder
        - encoder has information of the relationship with vectors
        - Multiheaded attention: perform the same attention task multiple times
        - Positional Encoding: the output of the encoder is just a weight sum of value vectors. Independent of the sequence


