---
date: 2021-10-24
title: "Elastic Search Summary"
categories: 
 - MRC
tags:
 - MRC
 - Boostcamp
 - Retriver
author: Hyeong
description: How to Elastic Search
---
## 1. Types of Retrieval
- Boolean Retrieval: retrieves a document if it includes specified word
- Rank Retrieval: specify a weight for terms. The weight for words differs depending whether the term came from the context or query. The weighting strategy for the terms can vary.
- TF-IDF: compute weight of terms by considering the frequency of words (TF) and if the word advents only in a few documents give high weigt (IDF).
- BM25: a modified version of TF-IDF. Can do parameter tuning.

## 2. Elasticsearch
- Elastic search indexes each document by words, decreasing the time complexity from O(n) to O(1); index of all documents that include a word is saved. This method is called Inverted Index. 

#### a. Analyzer
- Before processing the query and returning the matching value, a function called analyzer in Easlticsearch preprocesses the input.
- Flow: Char Filters - Tokenizer - Token Filters
- Char Filters: filters characters such as html tokens before tokenizing
    - HTML Strip character filter
    - Mapping character filter
    - Pattern replace character filter
- Tokenizer: breaks down the words to smaller units of meaning. Can select from multiple choices
    - Word Oriented Tokenizer: standard, letter, whitespace
    - Partial Word Tokenizer: N-gram
    - Structured Text Tokenizer: Keyword
- Token Filter: removing tokenized units
    - remove words like 'the', which does not have meaning
    - put words that has different form but is basically the same word
    - includes filters such as stemmer, n-gram, stop-words, shingle, uppercase, lowercase

#### b. Settings
- Scoring: computes score to return documents that best match the query
    - Default is BM25, but can use DFR, DFI, IB, LM Dirichlet


