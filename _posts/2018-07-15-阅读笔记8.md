---
layout: post
title: Bidirectional Recurrent Convolutional Neural Network for Relation Classification
category: Extraction
tags: Paper Reading
description: Bidirectional RNN
---
@Author
Rui Cai, Xiaodong Zhang and Houfeng Wang∗

ALC 2016

## Introduction
本文的模型BRCNN是为了 **给句子中两个实体的关系分类**   
<font color=#ff7f50>这是不是就意味着大前提就是一个句子中存在两个有关系的实体？ 那么实体是作者自己找吗还是自带</font>

一些以来，一些SOA系统专注于对两个实体间的SDP建模来对CNN或者RNN来做变动。
我们的工作更多的是通过结合CNN和two-channel RNN with LSTM 来充分利用SDP间的dependency relation信息

总之，我们提出了一个利用 沿着SDP前向和后向的方向信息 的双向结构来学习 关系表示， 这对 **关系的方向分类** 来说是有益的
## 贡献
1. 第一次在信息抽取中引入了深度残差网络
2. 大幅度提升了CNN，并包含一个SOA结果
3. 本文的identity mapping with shortcut feedback 可以方便地被应用于关系抽取任务中的各种CNN变体


## 相关工作

2005年， Bunescu and Mooney就通过SDP来捕获predicate-argument sequences，这为关系分类提供了有利的证据。


作者注意到在SDP中，每两个相邻的词 $w_{a}$  $w_{b}$ 会被一个依赖关系 $r_{ab}$ 连接起来。
支配词和它的孩子之间的依赖关系在意义上很不一样，另外，如果调查一下SDP，它对应着相同的关系，并且同方向。


第二个贡献就是提出了BRCNN，利用SDP的前后向信息来学习表现，这也 **加强了关系的方向分类能力**

## 题外话

卷积神经网络旨在概括关系提及的局部和连续上下文，而递归神经网络通过存储器单元自适应地在整个句子中累积上下文信息，从而编码用于关系分类的全局和可能不连续的模式。

## 模型

BRCNN分为一个前向RCNN和一个后向RCNN（就是SDP的前后向）

然后每个RCNN中又有两个LSTM（two channel LSTM），一个给SDP embedding，一个给word embedding，互不干扰，在卷积层连接汇合

## 实验
We evaluate our method on the SemEval-2010 relation classification task, and achieve a state-ofthe-art F1-score of 86.3%.

## 结论
深度CNN对噪声NLP问题有积极作用


## 启发

可以在噪声上下文章
1. 源头上减噪，训练集，比如说多示例学习
2. 带着噪声可以训练吗？ 在训练中消除噪声的影响
3. 在最后output部分或者pooling部分消除噪声的影响
