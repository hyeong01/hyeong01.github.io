---
date: 2021-09-24
title: "[AI Boostcamp Day 36] Special Lectures"
categories: 
 - Naver AI Boostcamp Diary
tags:
 - Career
 - Kaggle Competition
 - Quant Trading

author: Hyeong
description: ML Developer Career
---
### Career as a ML Developer?
- ML modeling is getting more and more automated. Should learn other technical stacks as well. 
    - FE abilities for making annotation tools and debugging tools
    - BE abilities for api serving, massive gpu training
    - NLP -> CV, model lightening
- Full Stack ML Engineer
    - Front-end + Back-end (API server, DB) + ML model (server)
    - Full stack Engineer with ML capabilities
    - ML capabilities include the ability to understand deep learning research and implement the model.
    - Roadmap
        - Stacks are getting easier (Vue, PyTorch, Django)
        

### How to Win Kaggle and Other Competitions?
- Validation strategy is important. One example is k-fold valdiation. The validation score is the average of k datasets. Might have to try stratified k-fold, just in case where classes biased depending on the folds.
- Generally Accepted Best Strategy for Ensemble:
    1. Stratified k-fold Ensemble (same model architecture)
    2. Differnt Model Ensemble
        - ML model + DL model (LightGBM, XGBoost, NNs)
        - LSTM + BERT + GPT2, RoBert
        - Resnet, Efficientent, Resnext
        - Greater synergy if the models are more different!
    3. Use weighted sum for blending
    4. The performance of a single model should also be decent. Should devote signifcant time, which is about one to two weeks for kaggle, to the ensembl process

### ML Product
- Objective -> Data Collection -> ML Model Development -> Model Serving