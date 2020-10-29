---
layout: post
title: HMM MEMM CRF
category: Extraction
tags: Paper Reading
description: sentence-level
---
* content
{:toc}


对于HMM的话，其判断这个标注成立的概率为 
$P= P(s转移到s)*P('我'表现为s)* P(s转移到b)*P('爱'表现为s)* ...*P().$训练时，要统计状态转移概率矩阵和表现矩阵。

对于MEMM的话，其判断这个标注成立的概率为$ P= P(s转移到s \|'我'表现为s)*P('我'表现为s)* P(s转移到b\|'爱'表现为s)*P('爱'表现为s)*.. $训练时，要统计条件状态转移概率矩阵和表现矩阵。

对于CRF的话，其判断这个标注成立的概率为 $P= F(s转移到s,'我'表现为s)....$F为一个函数，是在全局范围统计归一化的概率而不是像MEMM在局部统计归一化的概率。



#### 从HMM到MEMM
由于HMM的两个假设：观测独立，隐藏状态只受前一个隐藏状态影响
观测独立造成了HMM的一个缺点，也就是某个观测结果只受当前隐藏状态的影响
我们希望取消观测独立的假设，让某个观测结果能受到多个隐状态的影响
如下图
![enter description here](https://raw.githubusercontent.com/ZhaoKangkang0572/imgbed/master/小书匠/1603939112168.png)
这时，表达式由
$$
P(O,I)=\prod \limits_{j}^{n}P(I_j\|I_{j-1})P(O_j\|i_j)
$$
变为
$$
P(O,I)=\prod \limits_{j}^{n}P(I_j\|I_{j-1})P(O\|I_1,I_2,...,I_n)\\
=P(O_1\|I_1,I_2,...,I_n)*...*P(O_n\|I_1,I_2,...,I_n)*\prod \limits_{j=1}^{n}P(I_j\|I_{j-1})
$$

但是，这样的话，对于每一个$P(O_n\|I_1,...,I_j)$,如果使用有监督方法去统计的话，很有可能无法出现概率为0的情况，而如果使用EM算法的话,即便算出来了，也无法算出$P(O_n\|I_j)$

这时，MEMM出场了，他将模式转换成易于计算的判别式
![enter description here](https://raw.githubusercontent.com/ZhaoKangkang0572/imgbed/master/小书匠/1603940297825.png)
## Reference
https://www.cnblogs.com/hellochennan/p/6624509.html
https://zhuanlan.zhihu.com/p/159165806