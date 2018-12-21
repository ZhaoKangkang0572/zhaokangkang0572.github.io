---
layout: post
title: End-to-End Relation Extraction using LSTMs on Sequences and Tree Structures
category: Extraction
tags: Paper Reading
description: Cross-Sentence N-ary, Graph LSTMs
---

## 一句话概括（？）
用了端到端的神经网络来抽取实体和他们之间的关系（2016年这个方法很新吗，为什么感觉端到端没啥新意）
通过在bidirectional sequential LSTM-RNNs上堆叠bidirectional trees tructured LSTM-RNNs，本文中基于RNN的模型能捕获，词序以及依赖树子结构信息。
这使得本文的模型可以通过单个模型中分享的参数来联合表达实体和关系。


另外，我们也鼓励通过 **实体预训** 和 **预定抽样** 来实现 **训练中的实体检测** 以及 **关系抽取中的实体关系利用**

## 引言

传统（简单认为是2010之前的）方法将关系抽取分成两步来做：NER和关系抽取。
但是近来的研究把它作为端到端的任务来并且取得来很好的结果，原因是关系与实体是紧密相连的。

使用NN来呈现实体间的关系有两种方法：  CNN，RNN   
RNN可以表现 **（基本的语言结构）essential linguistic structures**， 但是从先行研究的结果来看，LSTM based RNN 比CNN要差。

先行研究里基于LSTM的RNN只包含了有限的语言结构和神经结构，**并没有将关系和实体一起表现出来**（为什么没有表现出来）

本文：一个包含了互补语言结构的LSTM

## 亮点


## 启发

果然最重要的还是在如何捕获文本信息上，本文可以较好地捕获依赖树，词序信息。
