---
layout: post
title: Neural Relation Extraction with Selective Attention over Instances
category: Extraction
tags: Paper Reading
description: sentence-level
---
@Author   

Yankai Lin1, Shiqi Shen1, Zhiyuan Liu1,2∗ , Huanbo Luan1, Maosong Sun   
ACL 2016



## Introduction
开篇又是把远程监督吊打一遍--- <font color=#ffff00>wrong labeling problem </font>

说为了解决这个问题，提出了sentence-level attention-based model。<font color=#FF7F50> 不明白为什么句子级别模型的可以解决这个问题。</font>   


这篇文章为 **distant supervised** 关系抽取提出了一个 **基于注意力机制的句子级别的CNN**   
主要是使用CNN来对句子的语义信息进行编码，之后，为了利用所有有用（informative）的句子，本文将关系表示为句子嵌入（sentence embedding）的语义组合。<font color=#FF7F50> 两个问题，第一个句子嵌入的语义组合是什么，第二个，怎么找到有用句子</font>   
然后为了解决 **Wrong Labeling Problem**  作者在多示例上构建了句子级别的注意力机制， 希望可以由此静态地减少噪声示例的权重。 。<font color=#FF7F50> 虽然还是不明白，但是开始了 </font>   
> “build sentence-level attention over multiple instances, which is expected to dynamically reduce the weights of those noisy instances.”   


## 相关研究  
这里提到一个多示例学习，主要应该就是问了减少错误训练数据带来的影响，先放一段话，回头仔细看   
> To alleviate the wrong labelling problem, (Riedel et al., 2010) models distant supervision for relation extraction as a multiinstance single-label problem, and (Hoffmann et al., 2011; Surdeanu et al., 2012) adopt multiinstance multi-label learning in relation extraction.

> **To the best of our knowledge, this is the first effort to adopt attention-based model in distant supervised relation extraction.**


## 模型

模型分两部分   
* Sentence Encoder    
主要就是用CNN来构建句子的分布表示

   * Vector Representation   
   注意这里也使用了position embeddings he word embeddings

   * Conv，pooling and Non-linear Layer   
   常规操作，无需赘言，可以学习一下引用方法

   ![](../../graph/The-architecture-of-CNN-or-PCNN-used-for-sentence-encoder.png)  
   到这个图为止，将句子信息编码为一个非线性层
* Selective Attention over Instances   
这里就是使用sentence-level attention 来选择相关句子<font color=#FF7F50>（应该就是前文的informative sentence, 难道就是用attention来选择有用的信息？）</font>   
   ![](../../graph/alternative-attention.png)



## 启发
