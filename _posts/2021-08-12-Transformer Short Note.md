---
date: 2021-08-12
title: "Transformer Short Note"
categories: 
 - DL Short Notes
tags:
 - RNN
 - Machine Learning
 - Deep Learning
 - Transformer
author: Hyeong
description: Transformer Model Basic Concepts
---

### Tramsformer:
- To solve the problem in dealing with sequential data; the input often changes in sequence and length
- Recursive x attententive o
- Encoder (attention)
![Imugr](https://i.imgur.com/JPxG6LA.png)
    - Not regressive
    - Create query vector, key vector, and value vector for each word
    - Dot product the query and key vector
    - Regularize it with the root dimension of key vector and use softmax
    - the weighted sum of value vectors is the output from the encoder
    - encoder has information of the relationship with vectors
    - Multiheaded attention: perform the same attention task multiple times
    - Positional Encoding: the output of the encoder is just a weight sum of value vectors. Independent of the sequence


