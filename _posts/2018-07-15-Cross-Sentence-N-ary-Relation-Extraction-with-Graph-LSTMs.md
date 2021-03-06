---
layout: post
title:  "Cross-Sentence N-ary Relation Extraction with Graph LSTMs"
date:   2017-11-17 13:31:01 +0800
categories: Relation Extraction
tag: Relation Extraction
---

* content
{:toc}

---
layout: post
title: Cross-Sentence N-ary Relation Extraction with Graph LSTMs
category: Extraction
tags: Paper Reading
description: Cross-Sentence N-ary, Graph LSTMs
---

## 一句话概括
本文使用一个Graph LSTMs来实现跨句多元关系抽取。
![enter description here](https://raw.githubusercontent.com/ZhaoKangkang0572/imgbed/master/小书匠/1576148907035.png)

## 引言
前人的工作多是在单个句子上的二元关系抽取，限制了可用信息
过去的跨句信息抽取并不是真正对句子建模来获取关系匹配，而是使用**共指**来在多个句子中取得 *access to arguments*

## 亮点
通过采用graph  formulation，本文的模型包含基于链或树型LSTM的先行研究，并且结合一组丰富的语言分析来辅助关系提取。   
本文“opens up opportunities for joint learning with related relations.” 比如说，$d,g,v$ 里的回应关系也暗指了二元子关系：drug d 和mutation v。甚至在远程监督中，多元关系的监督信号比二元子关系的更稀疏。此方法使得多元关系和二元关系上的多任务学习更简单。
>请解释所谓的 **“一组丰富的语言分析”**

## 结论
在远程监督和监督学习中，比起其他神经网络变体和精心设计的基于特征的分类器，graph LSTMs可以编码更丰富的语言信息。
此外，带有sub-relations的多任务学习进一步提升了效果，句法分析为graph LSTM的性能带来了显着的好处，特别是在语法准确性很高时。



## 方法
> to the best of author's knowledge, graph LSTMs还没有被应用到NLP任务中。

![](../../graph/A-GENERAL-ARCHITECTURE-FOR-GRAPH-LSTMS.png)  
### graph LSTMS

词向量作输入   
然后graph lstms学习每个单词的上下文表示  
对于被讨论的entity，他的上下文表示被连接（concatenation）起来作为分类器的输入  
对于多单词的entity就简单地将词向量平均一下，作者说：将更复杂的聚合方法的探索留给未来的工作吧   
graph LSTMS的核心是一个可以捕获input words上不同dependencies的document graph  
根据dependencies来包含document graph， graph LSTMs包含了linear-chain or tree LSTMs。  

缺点：
1. graph中有环使得反向传播成为问题
2. graph中边太多使得调参成为问题

### documetn graph
document graph 是为了对语言分析中各种dependencies建模，它可以捕获句内和句间的dependencies，

### 反向传播
这一节不想看了，有空再说



## 先行研究
作者指出，在标准二元关系设定中，优势方法通常是根据在讨论中的两个关系中的最短路径，或者从路径中通过导出丰富的特征，又或者通过神经网络建模。

由于这里有 $C(n,2)$ 条路径，所以将这种范式概括n-ary setting是具有挑战性的，一个由戴维森的语义学启发的明显的解决方法就是：首先，找出一个可以表示整个关系的trigger短语，然后减少trigger和argument之间的n元关系到二元关系。
但是，这样仍然存在问题：通常难以识别一个trigger，因为关系是被多个通常不相连的词共同表现的。
更甚者，标注训练样本耗费时间金钱，特别是要求trigger的时候，

## 启发
 这个更复杂的作者留给未来聚合方法我可以有一点想法
