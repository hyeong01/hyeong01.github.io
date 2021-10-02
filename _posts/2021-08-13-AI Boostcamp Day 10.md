---
date: 2021-08-13
title: "AI Boostcamp Day 10"
categories: 
 - Naver AI Boostcamp Diary
tags:
 - GAN
 - Generative Models
author: Hyeong
description: Basic Pytorch Implementation
---

### What I studied today:
1. Generative Model?
- Not only confined to generation of images or videos
- Classification model is a form of generative model (explicit model)
- Generative model that prodcudes images and videos are called implicit model
2. Independence and Number of Parameters
- If we assume independence of parameters we can compress the number of parameters. For example, for a picture with n pixels, number of possible states are <img src="https://latex.codecogs.com/gif.latex?2^{n}" title="2^{n}" />. However, if we can assume independence, only n parameters can describe the whole information. This is because each pixel can be described with a single parameter, and since they are all independent the necessary information needed to describe the whole information is a sum.
- But this assumption of independence is too strong. Instead we can try assuming conditional independence. If we hold Markov assumption (the assumption that the parameter is only dependent on the parameter right before), the number of parameters can be reduced down to 2n-1
3. Auto Regressive Model
- Considers the data that comes before.
- We need a sequence of all random variables to implement AR model. Need to know what comes before
- Neural Autoregressive Density Estimator Model
    - ![Imgur](https://i.imgur.com/OxkNxM7.png)
    - Nth output is dependent on inputs from 1 to N-1
    - Can predict the density of each variables
4. Latent Variable Models
- Autoencoder is not a generative model
- Variational Auto-encoder
    - What makes Variational Auto-encoder a generative model?
    - Finding Posterior distribution with variational distribution
    - ELBO? What? ---> Needs further study
    - We do not know the posterior distribution. So no loss function. Thus, maximizing the ELBO = minimizing the KL-divergence
5. Generative Adverserial Model
- Generative model tries to deceive the adverserial model, and the adverserial model tries to find out if the generative model's output is fake or not. They both become better models
    