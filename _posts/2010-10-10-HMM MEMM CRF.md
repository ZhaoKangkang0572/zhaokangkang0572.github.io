---
layout: post
title: HMM MEMM CRF
category: Extraction
tags: Paper Reading
description: sentence-level
---
* content
{:toc}


对于HMM的话，其判断这个标注成立的概率为 $P= P(s转移到s)*P('我'表现为s)* P(s转移到b)*P('爱'表现为s)* ...*P().训练时，要统计状态转移概率矩阵和表现矩阵$。

对于MEMM的话，其判断这个标注成立的概率为$ P= P(s转移到s|'我'表现为s)*P('我'表现为s)* P(s转移到b|'爱'表现为s)*P('爱'表现为s)*..$训练时，要统计条件状态转移概率矩阵和表现矩阵。

对于CRF的话，其判断这个标注成立的概率为 $P= F(s转移到s,'我'表现为s)....$F为一个函数，是在全局范围统计归一化的概率而不是像MEMM在局部统计归一化的概率。

<div class="mermaid">
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
</div>

#### 从HMM到MEMM
由于HMM的两个假设：观测独立，隐藏状态只受前一个隐藏状态影响
观测独立造成了HMM的一个缺点，也就是某个观测结果只受当前隐藏状态的影响
MEMM取消了观测独立的假设，让某个观测结果能受到多个隐状态的影响

graph HMM
	A-->B

## Reference
https://www.cnblogs.com/hellochennan/p/6624509.html