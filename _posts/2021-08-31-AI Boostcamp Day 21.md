---
date: 2021-08-31
title: "[AI Boostcamp Day 21] Training, Training and Training"
categories: 
 - AI Boostcamp
tags:
 - P Stage
 - AI Stages
 - Training
 - PyTorch

author: Hyeong
description: About Tuning the DL Model
---
### What did I do today
 - Found wrong photos (labelled wrong from the first place) -> revised and distributed so that the teammates could use
 - Found out that the model was transforming not only the train data, but also the validation data in ways that it was intended to make the inference harder. Changed this.
 - Ran several models
    - AdamW vs SGD -> similar result, AdamW faster
    - mutliplicative LR scheduler vs CosineAnnealingLR scheduler -> cosine much better
    - simpler transformation vs compound transformation -> couldn't tell because of the problem mentioned above

### (Peer Session)[https://www.notion.so/2021-08-31-6555b9f9cb3f4c7485c1d545c3fe1156]

### Reflections
    - Make a plan always!


