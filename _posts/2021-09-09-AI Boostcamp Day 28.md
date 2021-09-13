---
date: 2021-09-09
title: "[AI Boostcamp Day 28] Seq2Seq, Beam Search, and BLEU Score"
categories: 
 - AI Boostcamp
tags:
 - U Stage
 - Boostcamp
 - NLP
 - Seq2Seq
 - Beam Search
 - BLEU Score

author: Hyeong
description: Advanced Concepts in NLP
---
### What did I learn today
1. Seq2Seq <br>
    ![Imgur](https://i.imgur.com/QLaOP5C.png)
    - [Image Source](https://proceedings.neurips.cc/paper/2014/file/a14ac55a4f27472c5d894ec1c3c743d2-Paper.pdf)
    - Takes a sequence of words as input and gives another sequence as an output
    - Composed of Encoder and Decoder
    - Decoder receives 'start of sentence' token at the beginning and gives 'end of sentence' token to end the sequence'
    - Problem? The huge volume of the sequence should be cramped into a netwrok even if the hidden dimension is relatively small + The information from the early sequence disappears! -> need of attention model
    
2. Seq2Seq Model with Attention <br>
    ![Imgur](https://i.imgur.com/32ZFTYi.png)
    - [Image Source](https://proceedings.neurips.cc/paper/2014/file/a14ac55a4f27472c5d894ec1c3c743d2-Paper.pdf)
    - Get hidden vectors from the encoder and a hidden vector from the decoder, and do inner product for each vector from the encoder with that from the decoder -> attention scores
    - With the attention scores, give corresponding weights to each hidden vector from the encoder. The weighted sum is the attention output
    - Attention output stacked to the decoder output constitutes the final output vector **y**
    - Teacher Forcing
        - In the decoder, the each layer feeds on the output from the previous layer
        - The model could either train on the output from the previous layer or use ground trugh instead. This is called teacher forcing
        - TF is faster, but less accurate 
    - Different Attention Mechanisms <br>
        ![Imgur](https://i.imgur.com/J3h020M.png)
        - [Image Source](https://proceedings.neurips.cc/paper/2014/file/a14ac55a4f27472c5d894ec1c3c743d2-Paper.pdf)
        - Luong: 
            - General: When calculating the weight, add a learnable matrix between the hidden state output from the encoder and the decoder.
            - Concat: Concat the two hidden state vectors from the encoder and the decoder, concat an feed to a neural network to calculate the weight
    - Attention is great!
        - Improves neural machine translation performance. Enables focusing on particular parts of the source (which hidden state vector). 
        - Solves bottleneck problem arising from the fact that previous models had to rely solely on the outputs of the last layer
        - Due to shorter gradient back propagation path, attention solves the vanishing graident problem
        - Provides interpretability just by consulting the attention weights

3. Beam Search
    - Greedy Decoding: getting output one by one. The problem is that the model cannot fix  the prior result even if it later know that the output was wrong
    - Exhaustive Search: Try all possible sequences of **y** with V^t possible number of cases -> to complex
    - Beam Search
        - In between greedy decodign and exhuastive search. On each time step of the decoder, select k most probable partial translations.
        - [Image Source](https://web.stanford.edu/class/cs224n/slides/cs224n-2019-lecture08-nmt.pdf)
        - Decision Standard <br>
            ![Imgur](https://i.imgur.com/8UderAU.png)
        - Keep the best k hypothsis each step <br>
            ![Imgur](https://i.imgur.com/kfFKiHa.png)
        - For each k hypothesis, get top k most likely words and calculate scores. So the number of cases temporarily become k^2
        - Decode until the model produces the <END> token
        - If some hypotheses complete ealier then others, save it and continue calculating others
        - The longer the sequence, the smaller the probability -> normalize by the length of the sequence
    
4. BLEU Score <br>
    ![Imgur](https://i.imgur.com/Flcfxkl.png)
    - Precision: from the answers the model produces, how many of them are right?
    - Recall: from the entire relevant answer, how many of them did the model discover?
    - Get F1-score (the harmnoic mean of precion and recall)
    - The problem -> does not consider the sequence of the output
    - Compute **N-gram** (one to four) overlap and apply geometric mean
    - Qualify the geometric mean by **brevity penalty**. Brevity penalty is the total precision that allows overlap, with the maximum cap of 1.