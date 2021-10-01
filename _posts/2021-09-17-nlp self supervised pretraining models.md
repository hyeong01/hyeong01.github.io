---
date: 2021-09-19
title: "NLP - Unsupervised Pretraining Models"
categories: 
 - NLP
tags:
 - NLP
 - AI Boostcamp
 - Pretraining Models
 - GPT
 - BERT

author: Hyeong
description: Pretraining Models
---
## Contents

1. [Self-Supervised Pre-Training Models](#1-self-supervised-pre-training-models)
- [GPT-1](#a-gpt-1)
- [BERT](#b-bert)
- [Pre-training and Fine Tuning of BERT](#c-pre-training-and-fine-tuning-of-bert)
- [GPT-1 vs BERT](#d-gpt-1-vs-bert)
- [Machine Reading Comprehension for BERT](#e-machine-reading-comprehension-for-bert)

2. [Advanced Self-Supervised Pre-Training Models](#2-advanced-self-supervised-pre-training-models)
- [GPT-2](#a-gpt-2)
- [ALBERT](#b-albert)
- [ELECTRA](#c-electra)
- [Light-weight Models](#d-light-weight-models)

## 1. Self-Supervised Pre-Training Models
The self-attention in transformers has been gaining popularity across the DL domain due to its high performance and versatility. Models that adopt the structure include BERT, GPT, ALBERT, ELECTra in the domain of NLP.

#### a. GPT-1
![Image](https://i.imgur.com/ZbkPlfY.png) <br>
[Image Source](https://cdn.openai.com/research-covers/language-unsupervised/language_understanding_paper.pdf)
- Introduced special tokens for start of the sentence, end of the sentence, or deliminators to cater to diverse tasks of transfer learning
- No need to use task-specific models for each task
- Train the transformer with LM (Language Model), and use the pretrained transformer like a lego block to structure the model for a specific task
- Attach a vector for extraction, feed into the network, and use the altered extraction vector to yield the result

![Image](https://i.imgur.com/7rAi0Ze.png) <br>
[Image Source](https://cdn.openai.com/research-covers/language-unsupervised/language_understanding_paper.pdf)
- Outperformed all other contemporary SOTA models in almost all tasks.

#### b. BERT
![Image](https://wikidocs.net/images/page/35594/bert-openai-gpt-elmo-%EC%B6%9C%EC%B2%98-bert%EB%85%BC%EB%AC%B8.png)
[Image Source](https://arxiv.org/abs/1810.04805)
- GPT has the problem of not taking into account the sequences that come either before or after the current time period
- To solve this problem, BERT introduced MLM (Masked Language Model) for pretraining, a bi-directional language model. Usually in bi-directional models, the model can cheat by looking at the answers from future sequences. However, MLM prevents this by replacing a word with a [Mask] token. In speicifc, the researchers set the masking ratio to 15%, and within that 15% percent of masked words, left the masked token unchage 80% of the times, 10% of the times replaced the word with a random word, and for the other 10% kept the same sentence. This was because the model would not find a [Mask] token in the pretraining stage, and the researchers wanted the model to be prepared for such an environment
- Another type of dataset the reseachers used for pretraining was NSP (Next sentence Predition), in which task that the model has to decide whether the two sentence were together originally, or a stack of two random sentences.
- Used WordPiece embeddings
- For positional embedding, BERT did not use predifined sinusoidal functions. Rather, it uses trainable positional embedding
- When the model has two sequences to process, the model adds addtional embedding vector to the sequences. Add 0 to the first sequence for all embedding vectors, and 1 to the next sequence.

#### c. Pre-training and Fine Tuning of BERT
![Image](https://i.imgur.com/Nwb6Zv4.png) <br>
[Image Source](https://arxiv.org/pdf/1810.04805.pdf) <br>
- Pretrain on MLM and NSP simultaneously. Use the [CLS] token to get the answer for NSP task, and the other outputs for MLM task. <br>

![Image](https://i.imgur.com/E1b8apq.png) <br>
[Image Source](https://arxiv.org/pdf/1810.04805.pdf) <br>
- The process is similar for task-specific transfer learning, with changes on the format of input vector and the vectors the model uses to pin down the answer.

#### d. GPT-1 vs BERT
![Image](http://www.jajsmith.ca/images/bert/glue-tests.png) <br>
[Image Source](https://arxiv.org/pdf/1810.04805.pdf) <br>
- Data Size for Pretraining
    - GPT: BookCorpus (800M Words)
    - BERT BookCorpus + Wikipedia (2500M Words)
- BERT learns A/B embedding (sentence differentiation) during pretraining
- Batch Size: Larger the better for performance
    - GPT: 32000 words
    - BERT: 128000 words
- BERT uses different learning rates for each fine-tuning experiments. GPT uses the same learning rate for all tasks

#### e. Machine Reading Comprehension for BERT
- BERT is not confined to predicting missing words. The model can be trained to understand a given passage and answer a question regarding that passage.
- Use [CLS] token to check if the answer is in the passge. Then the model specifies a start vector and an end vector, which were previously input vectors of a sequence. The phrase between the two vectors is the answer.

## 2. Advanced Self-Supervised Pre-Training Models
#### a. GPT-2
- Much larger than GPT-1, but still trained with LM
- High quality dataset
- Divided the weights of residual layer with <a href="https://www.codecogs.com/eqnedit.php?latex=\sqrt{n}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sqrt{n}" title="\sqrt{n}" /></a> 
- Aimed for performing specific tasks on a zero-shot setting. The model does not need additional modification nor transfer learning to perform specific tasks.
    - To summarize, ask the model "what is the summary of a given passage"
    - To classify the sentiment, ask the model "what is the sentiment of a given sentence"
    - We do not ask actual questions to the model. We rather add a token or a phrase such as TL;DL (too long did not read) to summarize, but the point is that any task is essentially presented in the form of a question, so we do not need different structures for different tasks. 

#### b. ALBERT
The size of language models were getting gigantic, need to reduce the size while retaining decent performance. ALBERT suceeded in surpassing the SOTA models with a lighter model <br>
![Image](https://i.imgur.com/J1HylL9.png) <br>
[Image Source](https://openreview.net/pdf?id=H1eA7AEtvS)
- Factorized Embedding Parameterization <br>
[reference](http://isukorea.com/blog/home/waylight3/446) <br>
    - <a href="https://www.codecogs.com/eqnedit.php?latex=V" target="_blank"><img src="https://latex.codecogs.com/gif.latex?V" title="V" /></a>: Vocab size
    - <a href="https://www.codecogs.com/eqnedit.php?latex=H" target="_blank"><img src="https://latex.codecogs.com/gif.latex?H" title="H" /></a>: Hidden state dimension
    - <a href="https://www.codecogs.com/eqnedit.php?latex=E" target="_blank"><img src="https://latex.codecogs.com/gif.latex?E" title="E" /></a>: Word embedding dimension
    - Hidden-state dimension should be the same as word embedding dimension due to the residual connection
    - In order to transform the word embedding to <a href="https://www.codecogs.com/eqnedit.php?latex=H" target="_blank"><img src="https://latex.codecogs.com/gif.latex?H" title="H" /></a> sized vector, we end up with a matrix with the size of <a href="https://www.codecogs.com/eqnedit.php?latex=V*H" target="_blank"><img src="https://latex.codecogs.com/gif.latex?V*H" title="V*H" /></a>. However, if we factorize this into two vectors with the size of <a href="https://www.codecogs.com/eqnedit.php?latex=V*E" target="_blank"><img src="https://latex.codecogs.com/gif.latex?V*E" title="V*E" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=E*H" target="_blank"><img src="https://latex.codecogs.com/gif.latex?E*H" title="E*H" /></a>, we can save up memory as long as <a href="https://www.codecogs.com/eqnedit.php?latex=E" target="_blank"><img src="https://latex.codecogs.com/gif.latex?E" title="E" /></a> is much samller than <a href="https://www.codecogs.com/eqnedit.php?latex=H" target="_blank"><img src="https://latex.codecogs.com/gif.latex?H" title="H" /></a>.
- Cross-layer Parameter Sharing <br>
Many layers, can share parameters across layers

![Image](https://i.imgur.com/hWrvhX8.png) <br>
[Image Source](https://openreview.net/pdf?id=H1eA7AEtvS) <br>
- Shared-FFN: sharing only the feed-forward parameters. Networks that process the <a href="https://www.codecogs.com/eqnedit.php?latex=H" target="_blank"><img src="https://latex.codecogs.com/gif.latex?H" title="H" /></a> in [here](https://hyeong01.github.io/nlp/nlp-transformer/#b-detailed-process)
- Shared-attention: sharing only the attention parameters. Networks that produces the <a href="https://www.codecogs.com/eqnedit.php?latex=H" target="_blank"><img src="https://latex.codecogs.com/gif.latex?H" title="H" /></a> in [here](https://hyeong01.github.io/nlp/nlp-transformer/#b-detailed-process)
- All-shared: sharing all

#### c. ELECTRA
![Image](https://imgur.com/df8WBqW.png) <br>
[Image Source](https://openreview.net/pdf?id=r1xMH1BtvB) <br>
- Similar to the idea of GAN
- Pretrain the encoder model as a discriminator, the main network
- The discriminator tries to find out if the generator, usually a small MLM model, replaced the word or not.

![Image](https://i.imgur.com/gNAF4ca.png) <br>
[Image Source](https://openreview.net/pdf?id=r1xMH1BtvB) <br>
- Surpasses MLM models

#### d. Light-weight Models
Aims to use language models on light devices such as mobile devices.
- DistillBERT: learns on soft labels that the teacher model produced
- TinyBERT: tries to mimic the outputs within the learning stages such as the key vector transformation matrix. The dimension is different because TinyBERT is a smaller model. Uses fully connected layer to channel the output of the teacher model into the student model. The parameters of the fully connected layer is also trainable.


