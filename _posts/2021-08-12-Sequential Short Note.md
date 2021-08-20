---
date: 2021-08-12
title: "Sequential Short Note"
categories: 
 - DL Models
tags:
 - RNN
 - Machine Learning
 - Deep Learning
 - Sequential Models
author: Hyeong
description: Sequential Model Basic Concepts
---

### Sequential Model:
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
- LSTM:
    - Devised to prevent the shorterm dependemncy problem of RNN
- GRU:
    - No cell state unlike LSTM
    - Hidden state itself is an output
    - Less parameter than LSTM -> better performance than LSTM


