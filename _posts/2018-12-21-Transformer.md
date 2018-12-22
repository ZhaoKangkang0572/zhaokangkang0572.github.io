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
这里主要介绍模型架构
周末再写一篇复现的

## 引言
本文放弃了循环和卷积结构，提出一个只有attention的模型：transformer

## 模型结构
transformer由encoder和decoder组成
给定输入 $$(x_1,...,x_n)$$,编码为 $$z=(z_1,...,z_n)$$ decoder会同时生成输出序列 $$(y_1,...,y_m)$$ 在每一步，模型都是自回归(auto-regessive)的: 利用前一步生成的symbol作为下一步输出的额外输入。

模型结构如下
![/styles/images/transformer/Transformer-model-architecture.png]({{ '/styles/images/transformer/Transformer-model-architecture.png' | prepend: site.baseurl }})  

### 编码栈
encoder stack由6个结构图左边部分堆砌而成。这六层中，每一层有两个子层。一个子层是auto-regressivemulti-head self-attention，另一个是position wise fully connected feed-forward network. 在各个子层中采用残差(residual connection)加上标准化(normalization)的方式进行连接  
每个子层的输出 $$d_{model}=512$$

emcode stack 如图右侧所示，也由六层组成，每一层在上述两个子层外，额外插入了第三个子层，用来对encoder的输出进行multi-head attention操作。和encoder一样，每一个子层后面都采用标准化的残差连接。  
注意  
>为了防止位置参与到后续位置中，修来了decoder中的self-attention子层
>这个技巧（masking）结合output embeddings被偏移（offset）一个位置，确保了对于位置i的预测只依赖于位置i前面的部分，mask就意味着遮住后面的信息，
>是不是意思是虽然output是一起得到的，但是meige位置i的预测还是会依赖（0-i）的信息

### Attention
attention函数可以被描述成 $$query$$ 和 $$Key-Value对$$ 之间的映射
output被计算为values的加权和，其中分配给每个value的权重由query和相应的key通过compatibility function计算得来

### Scaled dot-product attention
结构如下  
![/styles/images/transformer/Scaled-Dot-Product-Attention.png]({{ '/styles/images/transformer/Scaled-Dot-Product-Attention.png' | prepend: site.baseurl }})   
输入 $$q,k,v$$,  $$d=n*m$ $
对于每一个单词的向量编码 $$e_i$$,分别用 $$W_q,W_k,W_v$$映射得到 $$q_i,k_i,v_i$$  
输出 对$$e_i$$的输出，这个输出是什么呢，是一个矩阵，里面装着对各个单词的注意力输出  
重点是对中间公式的理解,这里用实例代入看一下矩阵变换情况
$$Attention(Q,K,V)=softmax(\frac{QK^T}{\sqrt{d_k}})V$$    
这个公式的目的是：
>想要利用V来对Q进行操作，
>但首先要利用Q和K来决定V的哪一部分需要被重视   

```
import numpy as np
def softmax(x):
    exp_x = np.exp(x)
    softmax_x = exp_x / np.sum(exp_x)
    return softmax_x

# 假设我们有n个单词，每个单词的向量为m
设：
n=4
m=3
#词向量矩阵e e.shape=(4,3)
e=np.random.rand(4,3)

#现在通过它得到QVK

#每个单词的向量编码长度为4，我们将映射矩阵设为3*2
Wq=np.random.rand(3,2)
Wv=np.random.rand(3,2)
Wk=np.random.rand(3,2)

#利用映射矩阵得到QVK
Q=np.dot(e,Wq)
K=np.dot(e,Wk)
V=np.dot(e,Wv)

#QVK的长度为2，shape=(4,2)
# print(Q.shape)=(4, 2)
#也就是现在有了4个单词映射得到的QKV，每个单词的映射长度为2
```   

>接下来就是做Q与K的转置的点乘,这一步的目的就是
>上面写的  首先要利用Q和K来决定V的哪一部分需要被重视   

```  
QK=np.dot(Q,K.transpose())
#得到 print(QK.shape)=(4,4) 这一步是理解的关键，这个4*4的矩阵意味着什么？
```

感谢知友@盛源车的图片,非常清晰明了,也就是每个单词给句子中每个单词打的注意力分，比如说I认为 have应该获得多少分，a应该得到多少分，dream应该得到多少注意力  
![/styles/images/transformer/QK.png]({{ '/styles/images/transformer/QK.png' | prepend: site.baseurl }})

```
#不考虑softmax以及dk的开方
QK_soft=softmax(QK)
print(QK_soft.shape)
# QK_soft.shape=(4, 4)
Z=np.dot(QK_soft,V)
print(Z.shape)
# z.shape=(4, 2)
```   

### Multi-Head Attention
这里的Multi-Head就是把上面的部分重复做几遍，，然后把输出合到一起  
多头注意允许模型关注来自不同位置的不同子表征子空间的信息。
>在只做一次的情况下，平均操作就会抑制这种情况。?? 大概能感觉出，有机会详细实验一下

## Reference

https://www.zhihu.com/search?q=attention%20is%20all%20you%20need&type=content
