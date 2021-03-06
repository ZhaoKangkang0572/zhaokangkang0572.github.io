---
layout: post
title: Neural Temporal Relation Extraction
category: Extraction
tags: Paper
description: 一个普通的神经网路关系抽取
---

## 一句话概括
本文使用神经网络来实现关系抽取并得到了state-of-the-art 。
test
## 结论
1. 只将token做为输入好过手工特征模型
2. CNN好过LSTM
3.  encoding relation arguments with XML tags outperforms a traditional position-based encoding

## 引言
没有形式化的电子健康记录就无法可信地调查药物不良反应，疾病进展和临床结果。
时间关系抽取就是用来建立一个时间轴以便绑定医学事件和发生的时间。

定义时间关系抽取包括：
1. 时间包含事件
2. 事件包含事件  


考虑以下句子：
1. Patient was diagnosed with a rectal cancer in May of 2010
2. During the surgery the patient experienced severe tachycardia

句子1中， May of 2010包含了诊断这个事件  
句子2中， 手术包含了心动过速


## 贡献
1. 提供了一个简单的方法来编码relation argument positions，然后证明CNNs and LSTMs在这个任务上的有效性  
2. 相对于先行state-of-the-art研究本文只是用token做为输入就取得了state-of-the-art  
3. 展示了当仅提供单词的词性标签而不是单词本身时，神经模型在提取时间关系方面可以非常有效。


## 方法
1. 向量化文本 $n\times d$ 做为输入
2. 使用 ***markup of the relation arguments*** 扩充 ***input token sequences*** 来调整此输入 markup应该就是给句子注词性   
例：  
**MAKEUP：** *Patient was \<e> diagnosed \</e> with a rectal cancer in \<t> may of 2010 \</t>* 表示该模型用于预测事件诊断与2010年5月之间的关系  
3. 时间信息抽取被建模为3分类问题，包含，被包含以及None


## 心得
 其实本文的makeup就是简化了训练过程，
 本来的逻辑是神经网络来完成文本中的单词与时间事件的映射，然后完成三分类的过程，但是本文直接将单词与时间事件的关系直接标注了，少了这一部分，神经网络的训练变得简单，得出state-of-the-art也不奇怪了。

 这点比较重要，可以借鉴作为novel点。
