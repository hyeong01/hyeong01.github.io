---
date: 2021-09-06
title: "[AI Boostcamp Day 26] Basic RNN, LSTM, GRU"
categories: 
 - Naver AI Boostcamp Diary
tags:
 - U Stage
 - Boostcamp
 - NLP
 - RNN

author: Hyeong
description: Tapping into NLP
---
### What did I learn today
 1. RNN <br>
    ![Imugr](https://i.imgur.com/a70C2NA.png) <br>
    - [image source](http://karpathy.github.io/2015/05/21/rnn-effectiveness/)
    - <a href="https://www.codecogs.com/eqnedit.php?latex=h_{t-1}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h_{t-1}" title="h_{t-1}" /></a>: prior hidden-state vector
    - <a href="https://www.codecogs.com/eqnedit.php?latex=x_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_t" title="x_t" /></a> input vector at time t
    - <a href="https://www.codecogs.com/eqnedit.php?latex=h_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h_t" title="h_t" /></a> current hidden-state vector
    - <a href="https://www.codecogs.com/eqnedit.php?latex=f_w" target="_blank"><img src="https://latex.codecogs.com/gif.latex?f_w" title="f_w" /></a> RNN function
    - <a href="https://www.codecogs.com/eqnedit.php?latex=y_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y_t" title="y_t" /></a> output vector at time t
    - <a href="https://www.codecogs.com/eqnedit.php?latex=y_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y_t" title="y_t" /></a> the occurance depends on the task. Sentiment analysis? -> t at the last time interval.

2. Types of RNN
    - One to Many: other than the single input time interval, zero-vector input!
    - Many to One: no <a href="https://www.codecogs.com/eqnedit.php?latex=y_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y_t" title="y_t" /></a> output except one time interval!
    - Many to Many 1: e.g. after reading the sequence input, output the translation of the given sentence
    - Many to Many 2: While receiving the input, output the result at spot!

3. RNN Characeter-level Language Model <br>
    ![Imgur](https://i.imgur.com/K35FY4G.png)
    - [image source](http://karpathy.github.io/2015/05/21/rnn-effectiveness/)
    - Straigh forward!
    - The larger the hidden laer dimension is, the more information the network retains!
    - Very time & resource comsuming because the network has to forward the entire seuqene to get the loss and do deriviation to computet the gradient. -> break into smaller chunks and train with that.
    - Why we don't use RNNs: due to vanishing, exploding gradient problem. 

4. LSTM
    - Solves vanshing gradient problem!
    - Overall Model <br>
    ![Imgur](https://i.imgur.com/oN1Kotu.png)
        - [image source](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
        - <a href="https://www.codecogs.com/eqnedit.php?latex=c_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?c_t" title="c_t" /></a> (upper inflow from the prior model) has more information than the hidden state vector. 
        - <a href="https://www.codecogs.com/eqnedit.php?latex=h_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h_t" title="h_t" /></a> (below inflow from the prior model) mainly has information about the output of next layer and is used as an input for the output of next layer.
    - Variables
    ![Imgur](https://i.imgur.com/OVB3iNC.png)
        - [image source](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
        - Sigmoid: has value between 0 and 1. Decides what percentage the function will preserve from the intial value.
        - tanh: has value between -1 and 1. Used when conveying information
    - Forget Gate 
    ![Image](http://colah.github.io/posts/2015-08-Understanding-LSTMs/img/LSTM3-focus-f.png)
        - [image source](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
        - the elements of <a href="https://www.codecogs.com/eqnedit.php?latex=f_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?f_t" title="f_t" /></a> is between 0 and 1. Decides the ratio of information retention.
    - Gate Gate
    ![Image](http://colah.github.io/posts/2015-08-Understanding-LSTMs/img/LSTM3-focus-i.png)
    ![Image](http://colah.github.io/posts/2015-08-Understanding-LSTMs/img/LSTM3-focus-C.png)
        - [image source](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
        - why <a href="https://www.codecogs.com/eqnedit.php?latex=i_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?i_t" title="i_t" /></a> is multiplied? To remove excess information!
    - Output
    ![Image](http://colah.github.io/posts/2015-08-Understanding-LSTMs/img/LSTM3-focus-o.png)
        - [image source](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
        - Use tanh to present the result as an info
        - Utilize only the part of the info as an output
        - <a href="https://www.codecogs.com/eqnedit.php?latex=c_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?c_t" title="c_t" /></a> has all the info, even those that the model do not need at the present sequence.
        - Modifying <a href="https://www.codecogs.com/eqnedit.php?latex=c_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?c_t" title="c_t" /></a>, the model can get <a href="https://www.codecogs.com/eqnedit.php?latex=h_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h_t" title="h_t" /></a> that only has the information we need at the present sequence
    - Why use tanh? To give non-linearity!
    - Why tanh in specific? To prevent the vanishing graidnet problem!

5. GRU
![image](http://colah.github.io/posts/2015-08-Understanding-LSTMs/img/LSTM3-var-GRU.png)
    - [image source](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
    - Cell state and hidden state combined
    - The larger the input gate, <a href="https://www.codecogs.com/eqnedit.php?latex=z_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?z_t" title="z_t" /></a>, the more information is lost from the prior hidden state and vice versa.

6. Why GRU and LSTM no gradient vanishing & exploding problem?
    - Use addition, not redundant multiplication

### [Peer Session](https://www.notion.so/nlp-team-9/2021-09-07-cf3943dc63cb40b7a85283100591904a)


