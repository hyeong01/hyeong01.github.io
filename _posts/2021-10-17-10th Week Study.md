---
date: 2021-10-17
title: "MRC Summary"
categories: 
 - MRC
tags:
 - MRC
 - Boostcamp
author: Hyeong
description: 10th week study summary
---
## 1. What is MRC

#### a. MRC tasks
- Extractive Answer Task: finding answer from a designated document
- Descriptive Answer Task: finding answer without a designated document
- Multiple-choice Datasets: selecting answer from multiple choices

#### b. Challenges
- Multi-hop reasoning
- Unanswerable questions

#### c. Evalutation Metric
- Exact Match
- F1 Score: frequency of token overlap

## 2. Unicode & Tokenization

#### a. Unicode
- An uniform way of processing characters
- ex) U+AC00
- 'U+': means unicode
- 'AC00': hexadecimal code point

#### b. Encoding
- Formatting unicodes into binary numbers
- UTF-8, UTF-16, UTF-32
- The number indicate the number of bytes allocated for the represenation of each character

#### c. Tokenization
- Subword tokenization: breaking down unfrequented words and using the whole word when appears more frequently
- Byte-Pair Encoding: replace the most frequented word with a different character. Repeat it multiple times

## 3. MRC Types:
#### a. Selection Based
- Extract the answer from the document by slicing
- Model: classifier
- Loss: location of the answer

#### b. Generation Based 
- Model: Seq-to-Seq PLM
- Loss: compute F1 by comparing
- Bart: Bidirectional Encoder + Autoregressive (Uni-directional) Decoder
    - ![Image](https://i.imgur.com/EMN1NYE.png)
    - Bart is pretrained to reconstruct a text with noise such as sentence permutation and deleted or masked tokens

## Preprocessing for Generative MRC:
- Use natural language to replace the speical tokens
- ![Image](https://i.imgur.com/drwQVS3.png)
- Most generative models like Bart do not receive token_types_ids because speicifying it proved futile. Only input_ids and attention_mask


## 4. Postprocessing 
#### a. For Selection Based MRC 
1. Find the highest position predictions for start and end position respectively
2. Remove invalid composition
3. Descendingly sort the composition according to the score
4. Get Top-K
#### b. For Generation Based MRC
1. Decoding: the output of a prior step is the input of the current step
2. Since the model can generate multiple top-k tokens for each stage, several tatics to adopt
    - Greedy Search: search only the option with the highest probability for each token output
    - Exhaustive Search: search all top-k token outputs and its branches 
    - Beam Search: maintain only the top-k candidates. Eliminate the rest

## 5. Passage Retrieval
- Finding the right passage for a given query
- MRC could be broken down into two structures. A Retrieval System and a Answering system
- Use query embedding and passage embedding to yield similiarity score for each pair
#### a. Passage Embedding
- Sparse Embedding: BoW + TF-IDF. Each dimension corresponds to a specific word
    - Limits of Sparse Embedding: the dimension is too big, similarity of the tokens are not taken into consideration, and no Further training is possible
- Dense Embedding: 
    - Upsides of Dense Embedding: less dimension of a embedding vector. The embedding is similar if the meanings are close
    - Use the \<CLS> tokens NLP models like BERT to create an embedding and apply dot product between the query embedding and the passage embedding.
    - 
    - Better Dense Encoding?
        - Larger DPR
        - Larger Pretrained Model
        - Better data
        - Choosing harder negative samples!
            - Train the enocder with passages that have high TF-IDF score but is not an answer
