---
layout: post
title: Attention-Based Bidirectional Long Short-Term Memory Networks for Relation Classification
category: Extraction
tags: Paper Reading
description: word-level
---
@Author
Peng Zhou, Wei Shi, Jun Tian, Zhenyu Qi∗ , Bingchen Li, Hongwei Hao, Bo Xu
Institute of Automation, Chinese Academy of Sciences   
ALC 2016

## Introduction
现存两个问题，一个是大量依赖wordnet之类的词汇资源，一个是重要的信息会出现在句子的任何位置，难以捕获   
<font color="FFFF00"> 接上文的心得2，直接编码位置很难，但是可以用相对位置</font>

这篇是词语级别的，还有一篇句子级别的，为什么说这篇是词语级别的呢，因为attention以及lstm是作用在词语上的
## 贡献
BLSTM with attention可以自动聚焦到于分类有很大关系的words   



## 模型
(1) Input layer: input sentence to this model;   
(2) Embedding layer: map each word into a low dimension vector;   
(3) LSTM layer: utilize BLSTM to get high level features from step (2);   
(4) Attention layer: produce a weight vector, and merge word-level features from each time step into a sentence-level feature vector, by multiplying the weight vector;   
(5) Output layer: the sentence-level feature vector is finally used for relation classification

不多解释，常规操作
这是2016的ACL我记得应该BLSTM-attention很多了啊，难道是在relation extraction上没有过吗
