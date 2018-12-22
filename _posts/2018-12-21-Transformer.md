---
layout: post
title:  Transformer---attention is all you need
date:   2018-12-21 00:00:00 +0800
categories: DL
tag: paper transformer
---

* content
{:toc}

去年这篇文章出来的时候就挺火的，不过我一直没有仔细看过，直到这个月BERT的发布，才发现已经到不好好重新读一遍不行的地步了。
这篇文章对论文进行剖析，主要还是翻译为主，加入几点思考
周末再写一篇复现的。

## 引言
本文放弃了循环和卷积结构，提出一个只有attention的模型：transformer

## 模型结构
transformer由encoder和decoder组成
给定输入 $(x_1,...,x_n)$,编码为 $z=(z_1,...,z_n)$ decoder会同时生成输出序列 $(y_1,...,y_m)$ 在每一步，模型都是自回归(auto-reges,sive)的: 利用前一步生成的symbol作为下一步输出的额外输入。
> 这里没搞懂，我的理解是一个句子在encoder中一次性编码完成输入给decoder，decoder也一次性输出全部的序列，按这里讲的“利用前一步生成的symbol作为下一步输出的额外输入”不就和LSTM一样使用循环了吗。

模型结构如下

![/styles/images/transformer/Transformer-model-architecture.png]({{ '/styles/images/transformer/Transformer-model-architecture.png' | prepend: site.baseurl }})
### 编码栈

encoder stack由6个结构图左边部分堆砌而成。这六层中，每一层有两个子层。一个子层是auto-regressivemulti-head self-attention，另一个是position wise fully connected feed-forward network. 在各个子层中采用残差(residual connection)加上标准化(normalization)的方式进行连接  
每个子层的输出 $d_{model}=512$

emcode stack 如图右侧所示，也由六层组成，每一层在上述两个子层外，额外插入了第三个子层，用来对encoder的输出进行multi-head attention操作。和encoder一样，每一个子层后面都采用标准化的残差连接。  
注意  
>为了防止位置参与到后续位置中，修来了decoder中的self-attention子层
>这个技巧（masking）结合output embeddings被偏移（offset）一个位置，确保了对于位置i的预测只依赖于位置i前面的部分
>是不是意思是虽然output是一起得到的，但是meige位置i的预测还是会依赖（0-i）的信息

### Attention
attention函数可以被描述成 $query$ 和 $Key-Value对$ 之间的映射
output被计算为values的加权和，其中分配给每个value的权重由query和相应的key通过compatibility function计算得来

#### scaled dot-product attention
