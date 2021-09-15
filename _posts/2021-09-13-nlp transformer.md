---
date: 2021-09-13
title: "NLP - Transformer"
categories: 
 - NLP
tags:
 - NLP
 - AI Boostcamp
 - Transformer

author: Hyeong
description: Transformer
---
## Contents

<ol>
    <li> <a href="#1-former-rnns">Former RNNs</a> </li>
    <li> 
        <a href="#2-transformer">Transformers</a>
        <ul>
            <li> <a href="#a-key-components">Key Components</a> </li>
            <li> <a href="#b-detailed-process">Detailed Process</a> </li>
            <li> <a href="#c-scaling-the-dot-product">Scaling the Dot Product</a> </li>
        </ul>
    </li>
    <li><a href="#3-multi-head-attention">Multi-Head Attention</a> </li>
    <li><a href="#4-comparison-of-computational-resources">Comparison of Computational Resources</a> </li>
    <li><a href="#5-block-based-model">Block-Based Model</a></li>
    <li>
        <a href="#6-model-speicific-techniques">Model Speicific Techniques</a>
        <ul>
            <li> <a href="#a-normalization">Normalization</a> </li>
            <li> <a href="#b-positional-encoding">Positional Encoding</a> </li>
            <li> <a href="#c-warm-up-learning-rate-scheduler">Warm-up Learning Rate SchedulerPermalink</a> </li>
        </ul>
    </li>
    <li>
        <a href="#7-decoder">Decoder</a>
        <ul>
            <li> <a href="#a-detailed-process">Detailed Process</a> </li>
            <li> <a href="#b-masked-self-attention">Masked Self-Attention</a> </li>
        </ul>
    </li>
    <li><a href="#8-model-performance">Model Performane</a> </li>
</ol>

Transformer adopts the attention method of Seq2Seq with attention without the division of the encoder and the decoder. Concise model helps faster learning, and by stacking queries into a matrix, the model further boosts the computational speed, still obviating the long term dependency problem and considering the future input sequences.

## 1. Former RNNs
- RNN: the information propagates through multiple mathematic transformations, casuing long term dependency problem
- Bi-directional RNN: long term dependency problem still present, but each output can consider the words that will come after the present time step
- Transformer even solves the long term dependency problem 

## 2. Transformer
- Uses only the attention model from Seq2Seq as the main model
- 
- General Structure <br>
![Image](https://user-images.githubusercontent.com/38639633/108292428-6b7a0c00-71d7-11eb-80d8-66673d3e3cc7.png)

#### a. Key Components <br>  
![Image](http://jalammar.github.io/images/t/transformer_self_attention_vectors.png)
[Image Source](http://jalammar.github.io/illustrated-transformer/)

- **Query Vector**: a vector transformed from the input vector of the corresponding time period via <a href="https://www.codecogs.com/eqnedit.php?latex=W^Q" target="_blank"><img src="https://latex.codecogs.com/gif.latex?W^Q" title="W^Q" /></a> to calculate the weights of each value vector in producing the final output <a href="https://www.codecogs.com/eqnedit.php?latex=h_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h_t" title="h_t" /></a>.
- **Key Vector**: vector transformed from all input vectors via the matrix product with <a href="https://www.codecogs.com/eqnedit.php?latex=W^K" target="_blank"><img src="https://latex.codecogs.com/gif.latex?W^K" title="W^K" /></a>. The model will calculate the weight for each value vector by doing inner product of a query vector and key vectors.
- **Value Vector**: input vectors from all time period are transformed via to produce value vector <a href="https://www.codecogs.com/eqnedit.php?latex=W^V" target="_blank"><img src="https://latex.codecogs.com/gif.latex?W^V" title="W^V" /></a>. The weighted sum of these vectors is the output vector.

#### b. Detailed Process
- The model trains matrix <a href="https://www.codecogs.com/eqnedit.php?latex=W" target="_blank"><img src="https://latex.codecogs.com/gif.latex?W" title="W" /></a> 
    - <a href="https://www.codecogs.com/eqnedit.php?latex=x_i&space;\cdot&space;W^V&space;\rightarrow&space;v_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_i&space;\cdot&space;W^V&space;\rightarrow&space;v_i" title="x_i \cdot W^V \rightarrow v_i" /></a>
    - <a href="https://www.codecogs.com/eqnedit.php?latex=x_i&space;\cdot&space;W^Q&space;\rightarrow&space;q_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_i&space;\cdot&space;W^Q&space;\rightarrow&space;q_i" title="x_i \cdot W^Q \rightarrow q_i" /></a>
    - <a href="https://www.codecogs.com/eqnedit.php?latex=x_i&space;\cdot&space;W^K&space;\rightarrow&space;k_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_i&space;\cdot&space;W^K&space;\rightarrow&space;k_i" title="x_i \cdot W^K \rightarrow k_i" /></a>
- We first calculate the weight, where n is the length of the entire sequence. The result is probability (or ratio) that adds up to 1
    - <a href="https://www.codecogs.com/eqnedit.php?latex=weight_i&space;=&space;softmax(q_i\cdot&space;k_1;&space;q_i\cdot&space;k_m;&space;..&space;q_i&space;\cdot&space;k_n)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?weight_i&space;=&space;softmax(q_i\cdot&space;k_1;&space;q_i\cdot&space;k_m;&space;..&space;q_i&space;\cdot&space;k_n)" title="weight_i = softmax(q_i\cdot k_1; q_i\cdot k_m; .. q_i \cdot k_n)" /></a> 
- Multiplying each element of the weight vector with the corresponding value vector, we get the output vector
    - <a href="https://www.codecogs.com/eqnedit.php?latex=h_i&space;=&space;weight_i&space;\cdot&space;(v_i;v_m;..v_n)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h_i&space;=&space;weight_i&space;\cdot&space;(v_i;v_m;..v_n)" title="h_i = weight_i \cdot (v_i;v_m;..v_n)" /></a> (output vector for the ith time period)
- Entire process simplified, we get
    - <a href="https://www.codecogs.com/eqnedit.php?latex=h_i&space;=&space;A(q_i,&space;K,&space;V)&space;=&space;\sum_j(\frac{exp(q_i\cdot&space;k_j)}{\sum_r&space;exp(q_i\cdot&space;k_r)})v_j" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h_i&space;=&space;A(q_i,&space;K,&space;V)&space;=&space;\sum_j(\frac{exp(q_i\cdot&space;k_j)}{\sum_r&space;exp(q_i\cdot&space;k_r)})v_j" title="h_i = A(q_i, K, V) = \sum_j(\frac{exp(q_i\cdot k_j)}{\sum_r exp(q_i\cdot k_r)})v_j" /></a>
- We have multiple query vectors, so if we stack them and make matrix <a href="https://www.codecogs.com/eqnedit.php?latex=Q" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Q" title="Q" /></a>, the whole process is simplified as follows
    - <a href="https://www.codecogs.com/eqnedit.php?latex=H&space;=&space;A(Q,K,V)&space;=&space;softmax(QK^T)V" target="_blank"><img src="https://latex.codecogs.com/gif.latex?H&space;=&space;A(Q,K,V)&space;=&space;softmax(QK^T)V" title="H = A(Q,K,V) = softmax(QK^T)V" /></a>
    or equivalently,
    - <a href="https://www.codecogs.com/eqnedit.php?latex=(|Q|*d_k)*(d_k*|K|)*(|V|*d_v)&space;=&space;(|Q|*d_v)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(|Q|*d_k)*(d_k*|K|)*(|V|*d_v)&space;=&space;(|Q|*d_v)" title="(|Q|*d_k)*(d_k*|K|)*(|V|*d_v) = (|Q|*d_v)" /></a>
- Matrix multiplication is well optimized, making the self-attention model even faster
- The model has huge improvement from the previous RNNs, also because the inputs from long period ago are nto subject to multiple transformations. All inputs have equal path to the outpiut of whenever time period, solving the long term dependency problem.
- On top of that, the sequence can consider the inputs that would normally appear later, allowing more information of the context to be channelled into the model.

#### c. Scaling the Dot Product
- Method:
    - <a href="https://www.codecogs.com/eqnedit.php?latex=H&space;=&space;A(Q,K,V)&space;=&space;softmax(\frac{QK^T}{d_k^{1/2}})V" target="_blank"><img src="https://latex.codecogs.com/gif.latex?H&space;=&space;A(Q,K,V)&space;=&space;softmax(\frac{QK^T}{d_k^{1/2}})V" title="H = A(Q,K,V) = softmax(\frac{QK^T}{d_k^{1/2}})V" /></a>
- Rationale: let's assume the elements of <a href="https://www.codecogs.com/eqnedit.php?latex=Q" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Q" title="Q" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=K" target="_blank"><img src="https://latex.codecogs.com/gif.latex?K" title="K" /></a> are mutually independent and follows a normal distribution with mean 0 and variance 1. The variance of <a href="https://www.codecogs.com/eqnedit.php?latex=QK^T" target="_blank"><img src="https://latex.codecogs.com/gif.latex?QK^T" title="QK^T" /></a> is <a href="https://www.codecogs.com/eqnedit.php?latex=d_k" target="_blank"><img src="https://latex.codecogs.com/gif.latex?d_k" title="d_k" /></a>, the dimension of the matrices. Having huge variance is not good for training because then the weights would vary significantly, meaning that the output would reflect only some of the value vectors. To prevent this, the model divides <a href="https://www.codecogs.com/eqnedit.php?latex=QK^T" target="_blank"><img src="https://latex.codecogs.com/gif.latex?QK^T" title="QK^T" /></a> with <a href="https://www.codecogs.com/eqnedit.php?latex=d_k" target="_blank"><img src="https://latex.codecogs.com/gif.latex?d_k" title="d_k" /></a>, feeding the softmax function with an input with the mean of 0 and the vairnace of 1.

## 3. Multi-Head Attention
![Imgur](https://i.imgur.com/tXU0k1A.png) <br>
[Image Source](https://arxiv.org/pdf/1706.03762.pdf)
- Need: each attention layer specializes in encoding the input sequence. For example, a layer could specialize in understanding the relationship between a noun and its modifers.
- <a href="https://www.codecogs.com/eqnedit.php?latex=MultiHead(Q,&space;K,&space;V)&space;=&space;Concat(head_1,...head_h)W^o" target="_blank"><img src="https://latex.codecogs.com/gif.latex?MultiHead(Q,&space;K,&space;V)&space;=&space;Concat(head_1,...head_h)W^o" title="MultiHead(Q, K, V) = Concat(head_1,...head_h)W^o" /></a>
- <a href="https://www.codecogs.com/eqnedit.php?latex=head_i&space;=&space;Attention(QW_i^Q,KW_i^K,VW_i^V)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?head_i&space;=&space;Attention(QW_i^Q,KW_i^K,VW_i^V)" title="head_i = Attention(QW_i^Q,KW_i^K,VW_i^V)" /></a>

## 4. Comparison of Computational Resources
![Imgur](https://i.imgur.com/wxLuLhN.png) <br>
[Image Source](https://arxiv.org/pdf/1706.03762.pdf)
- <a href="https://www.codecogs.com/eqnedit.php?latex=n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n" title="n" /></a> is sequence length
- <a href="https://www.codecogs.com/eqnedit.php?latex=d" target="_blank"><img src="https://latex.codecogs.com/gif.latex?d" title="d" /></a> is dimension of representation
- <a href="https://www.codecogs.com/eqnedit.php?latex=k" target="_blank"><img src="https://latex.codecogs.com/gif.latex?k" title="k" /></a> is the kernel size
- <a href="https://www.codecogs.com/eqnedit.php?latex=r" target="_blank"><img src="https://latex.codecogs.com/gif.latex?r" title="r" /></a> is the size of neighborhood
- Self attention model requires larger number of computations, but the type of computation is matrix multiplication, thus requires less total time for training. In contrast, the recurrent model requires less number of computations, but the operation is sequential; the model has a series connection, making the total training time longer.

## 5. Block-Based Model
![Imgur](https://i.imgur.com/6RJWPAR.png) <br>
[Image Source](https://arxiv.org/pdf/1706.03762.pdf)
- Residual connection: Propagates x to after the multi-head attention layer. The layer is trained to learn the residual, <a href="https://www.codecogs.com/eqnedit.php?latex=f(x)-x" target="_blank"><img src="https://latex.codecogs.com/gif.latex?f(x)-x" title="f(x)-x" /></a>, not <a href="https://www.codecogs.com/eqnedit.php?latex=f(x)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?f(x)" title="f(x)" /></a>
- Layer normalization


## 6. Model Speicific Techniques
#### a. Normalization
![Imgur](https://i.imgur.com/Lo3Jclf.png) <br>
[Image Source](https://arxiv.org/pdf/1803.08494.pdf)
- Affine Transformation: <a href="https://www.codecogs.com/eqnedit.php?latex=x&space;\rightarrow&space;ax&plus;b" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x&space;\rightarrow&space;ax&plus;b" title="x \rightarrow ax+b" /></a>. The parameters are all trainable.
- Batch Norm: for each pertaining node, normalize the values from all batches collectively and affine transform.
- Layer Norm: normalize each words vectors, then affine transform each sequence vector like below.
![Imgur](https://i.imgur.com/kRdTHCu.png)

#### b. Positional Encoding
- Need: transformer produces the same output wherever the words are place, as long as the input words are the same. See <a href='#2-transformer'> the structure of transformer</a> to understand.
![Imgur](http://nlp.seas.harvard.edu/images/the-annotated-transformer_49_0.png) <br>
[Image Source](http://nlp.seas.harvard.edu/2018/04/03/attention) <br>
- Use sinusoidal functions, for example, use sine functions for the even dimensions, and consine for the others, with different frequencies for all dimensions and them to input vectors.

#### c. Warm-up Learning Rate Scheduler
![Imgur](http://nlp.seas.harvard.edu/images/the-annotated-transformer_69_0.png) <br>
[Image Source](https://arxiv.org/pdf/1803.08494.pdf)
- Offsets initial large gradient with small learning rate. The apex in the middle further pushes the model that could have settled for a local minimun.

## 7. Decoder
When do we need to perform tasks that require additional sequence input, such as translation, we use models with decoder.

#### a. Detailed Process
![Image](http://nlp.seas.harvard.edu/images/the-annotated-transformer_14_0.png) <br>
[Image Source](http://nlp.seas.harvard.edu/2018/04/03/attention) <br>
- The query vector is from the decoder, and the key vector and the value vector is the output of the encoder
- Use Masked decoder self-attention to produce query vector

#### b. Masked Self-Attention
- At the inference stage, the model does not have any access to inputs from the later sequence. To emulate such environment in the training process, the model has to block the access to the inputs from later sequence.
- This can be done by adequately masking the output from <a href="https://www.codecogs.com/eqnedit.php?latex=Softmax(QK^T)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Softmax(QK^T)" title="Softmax(QK^T)" /></a> as below. 
![Image](http://nlp.seas.harvard.edu/images/the-annotated-transformer_31_0.png) <br>
[Image Source](http://nlp.seas.harvard.edu/2018/04/03/attention) <br>
- Purple region is the elements of the matrix that the value is set as 0.
- Each row mathematically expressed, <a href="https://www.codecogs.com/eqnedit.php?latex=weight_i&space;=&space;softmax(q_i\cdot&space;k_1;&space;q_i\cdot&space;k_m;&space;..&space;q_i&space;\cdot&space;k_n)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?weight_i&space;=&space;softmax(q_i\cdot&space;k_1;&space;q_i\cdot&space;k_m;&space;..&space;q_i&space;\cdot&space;k_n)" title="weight_i = softmax(q_i\cdot k_1; q_i\cdot k_m; .. q_i \cdot k_n)" /></a>
- Simply put, <a href="https://www.codecogs.com/eqnedit.php?latex=q_i\cdot&space;k_m&space;=&space;0,&space;(i<m)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?q_i\cdot&space;k_m&space;=&space;0,&space;(i<m)" title="q_i\cdot k_m = 0, (i<m)" /></a>

## 8. Model Performance
![Image](http://nlp.seas.harvard.edu/images/the-annotated-transformer_113_0.png) <br>
- Reduces the training cost significantly
- BLEU score surpassed all SOTA models at year 2014 for the given task

