---
layout: post
title: LSTM+Attention 
category: MLTheory
tags: LSTM Attention
description: 总结下前Attention时代的模型结构
---
* content
{:toc}

#### 分类
LSTM+Attention的实现方式主要分两种
>1. 在decode阶段要利用前一步的生成，例如Seq2Seq翻译
>2. 一步生成结果，不利用前一步

#### 一步生成

这个就很简单
$$
(1)\quad  v_t=\tanh(wh_t+b) \\
(2)\quad  \alpha_t=softmax(v_t) \\
(3)\quad  c=\sum{h_t\alpha_t}
$$


#### 利用前一步



