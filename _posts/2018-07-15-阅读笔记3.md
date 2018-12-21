---
layout: post
title: Distant Supervision for Relation Extraction via Piecewise Convolutional Neural Networks
category: Extraction
tags: Paper Reading
description: Cross-Sentence N-ary, Graph LSTMs
---

@ authors   
Daojian Zeng, Kang Liu, Yubo Chen and Jun Zhao

EMNLP 2015



 title

## Introduction

There are two problems in distant supervision relation extraction.  
1. First problem is caused by knowledge base.

To solve this problem, distant supervised relation extraction is treated as a multi-instance problem. And add extra class--(uncertainty of instance labels is taken into account)

2.  The noise that originates from the feature extraction process can cause poor performance.(It appears in every paper! everyone said that! it is important, however, can this paper solve this? We will see!!)

To handle this, they avoid feature engineering and instead adopt NN. (OK, proposed in 2015, NN is not all we want yet )


做机器学习系统时生成训练集是一个挑战   
对此的解决方法：
1. 远程监督  
但是有两个缺点  
1.1远程监督假设太过强势，在数据库中有关系的两个实体不代表在句子中也有这种关系 比如   
数据库：我--喜欢--苹果   
句子 我喜欢苹果做的苹果汁   
在这里就是我--喜欢--苹果汁
2. 一些远程监督依赖上古时期传统NLP工具做的特征，但有错误。 Ryan T McDonald 提出了句子越长，精度下降的，所以说上古时期的特征不可取。


作者认为他这个PCNN可以解决这个问题

## 本文贡献
1. 探索了没有手工特征情况下的关系抽取   
2. 为远程监督关系抽取将 多示例学习 引入PCNNS
3. 一个piecewise max pooling 层来捕获两个实体间的结构信息。（干货）



## 模型
> <font color=#ff7f50> 远程监督关系抽取被公式化为多示例学习  </font>

![](../../graph/PCNNs.png)  

* vector representation

   * word 没什么可说的，常规
   * position  用pf来指定实体对， 一个PF被定义为 e1和e2(pf1 and pf2)的相对距离的 **结合**   
   ![](../../graph/PFs.png)   
   和词向量一样，pf1 和pf2随机初始化，然后做表，对照look up   
   * 结合看图   
* convolution   
> <font color=#ff7f50> When using a neural network, the convolution approach is a natural means of merging all these features </font>   

其他没啥好讲的

* Piecewise Max pooling   
传统max pooling操作是为了将前面的层合并   
但是，这个操作不适用于关系抽取任务   
单层max pooling太快了，一下就把这么多隐含层捡到一层，而且在捕获细粒度特征上显得太粗糙， 此外，单层max pooling 不足以捕获两个实体间的结构化信息。   
在关系抽取中，基于两个给定实体，我们可以将句子划分为三段。于是我们提出一个piecewise max pooling对这三段分别进行max pooling操作。
* 激活函数   
常规操作   
* 多示例学习   
为了减少错误标签的问题。



## 结论   
本文有一个分段的思想，也就是说想要更细粒度的特征，可以学习这篇文来组合拆分
1. 在max pooling在做文章，拆分句子分开pooling   
2. 输入，词向量和位置向量共同作为输入，对我来讲，如果搞什么树形RNN，是不是也可以将结构信息用向量形式编码
