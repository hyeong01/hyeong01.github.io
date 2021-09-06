---
date: 2021-08-31
title: "[AI Boostcamp Day 25] Tapping into NLP"
categories: 
 - AI Boostcamp
tags:
 - U Stage
 - Boostcamp
 - NLP

author: Hyeong
description: Tapping into NLP
---
### What did I learn today
 1. Academic Disciplines related to NLP
    - NLP
        - Low Level Parsing
            - Tokenization, stemming 
        - Word and Phrase Level Parsing
            - Dependency parsing, noun-phrase chunking
        - Sentence Level Parsing
            - Sentiment analysis
        - Multi-sentence and Paragraph Level
            - Question answering
            - Dialogue systems
            - Summarization
        - Text Mining
            - Document clustering
            - Highly related to computational social science
            - Extract useful information and insights from text
    - Trends of NLP
        - RNN models used to be popular in order to understand the sequence of the words in a sentence
        - Transformer models -> very powerful, change of paradigm
2. Pre-DL NLP
    - Bag of Words
        - Construct a lexicon of unique words
        - Encode words to one-hot vectors
    - NaiceBayes Classifier
        - classifying document
        - Using Bayes' Rule. Computing the probability that the set of words will occur in a specified class. Class with larger probability -> assign class!
3. Word Embedding
    - Word2Vec
        - Vectorizing similar words to a closer space
        - NLP models can utilize this position of words
        - The closer the words are in sentences, the more similar the values are
        - How does this work? (Image Source: *Distributed Representations of Words and Phrases and their Compositionality*)
        ![Imgur](https://i.imgur.com/qBTJula.png)
            - The length of dictionary = dimension of column vector x
            - x is a vector expression of a word
            - W1, W2 is subject to training
            - W1 column dimension = W2 row dimension = hidden dimension -> decides the quantity of information
            - Process: get a word pair or tuple with a sliding window, set it as a ground truth and train.
        - Image Source: Distributed Representations of Words and Phrases and their Compositionality
    - GloVe
        - Computes the co-occurrence matrix first and then trains accordingly -> faster training
        - Using A as a ground truth possibility for co-occurance for inner product of words
4. Types of RNN
    - 

### (Peer Session)[]

### Reflections
    - Make a plan always!


