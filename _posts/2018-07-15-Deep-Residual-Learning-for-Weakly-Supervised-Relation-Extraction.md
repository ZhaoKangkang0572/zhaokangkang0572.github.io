---
layout: post
title: Deep Residual Learning for Weakly-Supervised Relation Extraction
category: Extraction
tags: Paper Reading
description: weakly-supervised
---
@Author
Yi Yao Huang, William Yang Wang

ALC 2017

## Introduction
深度残差网络在噪声很多的NLP任务中的作用不容易理解   
所以本文设计了ResCNN，然后调查了此模型在 噪声远程监督信息抽取中的作用
此外，本文还发现，不同于公认的那样，深度残差网络在浅层网络一样有用，，甚至在9层的cnn中，identify mapping也能显著提升远程监督关系抽取性能



## 贡献
1. 第一次在信息抽取中引入了深度残差网络
2. 大幅度提升了CNN，并包含一个SOA结果
3. 本文的identity mapping with shortcut feedback 可以方便地被应用于关系抽取任务中的各种CNN变体




## 模型
![](../../graph/ResCNNForRelationExtraction.png)   

这里解释一下ResCNN部分
![](../../graph/ResInRESCNNForRelationExtraction.png)   


## 实验
词向量： word embeddings released by (Lin et al., 2016) which are trained on the NYT-Freebase corpus (Riedel et al., 2010).

数据集： NYT freebase larger dataset (Riedel et al., 2010).

## 结论
深度CNN对噪声NLP问题有积极作用


## 启发

可以在噪声上下文章
1. 源头上减噪，训练集，比如说多示例学习
2. 带着噪声可以训练吗？ 在训练中消除噪声的影响
3. 在最后output部分或者pooling部分消除噪声的影响
