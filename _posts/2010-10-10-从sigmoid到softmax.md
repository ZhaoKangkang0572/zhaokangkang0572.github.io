---
layout: post
title: 从sigmoid到softmax 
category: MLTheory
tags: machine learning thor
description: sentence-level
---

#### Sigmoid
$g(z)=\frac{1}{1+e^{-z}}$
>饱和性（两侧导数逐渐趋近于0）导致梯度消失
>非0均值，输出值大于零，捆绑效应
>计算慢


#### SoftMax
$Softmax(z_i)=\frac{e^{z_i}}{\sum_{j=1}^n {e^{z_j}}} \quad for \:  i \: in \:1,2,3,...,n$
> 累加为1
> Softmax可以视为一种soft版本的argmax(hardmax只有被选中的变量才有梯度，其他都没有梯度)



#### SoftMax和cross-entropy
>Cross-entropy本质上是用来衡量两个概率分布的距离
>比如说，$a\;b$ 两组变量
>$a=[1,2,3]$    $b=[2,4,6]$
>直接求l2距离的话，相差很大，但是对他们做cross-entropy的话，距离就是0

SoftMax和cross-entropy经常一起用的原因就在这里，SoftMax求的是概率分布，再用cross-entropy衡量概率分布之间的距离

cross-entropy公式：
$xcent(p,q)=-\sum_k{p(k)log{(q(k))}}$

here:
$log{(q(k))$就是logSoftMax

#### softmax实现：logSoftMax
1.原始版本
```python
def softmax(x)
	exps=np.exp(x)
	return exps/np.sum(exps)
```

但是这种方法需要计算指数，如果说我们的输入很大$10000,20000$，那么分母上就会是$e^10000+e^20000$
显然计算上会溢出

2. 可以给它乘上一个系数，缩小分子分母
$Softmax(z_i)=\frac{e^{z_i}}{\sum_{j=1}^n {e^{z_j}}}=\frac{Ce^{z_i}}{\sum_{j=1}^n {Ce^{z_j}}}=\frac{e^{z_i+log(C)}}{\sum_{j=1}^n {e^{z_j+log(C)}}}=\frac{e^{z_i+D}}{\sum_{j=1}^n {Ce^{z_j+D}}}$
这里的D可以随便选，一般选择$D=-max(a1,a2,...,an)$
```python
def stableSoftMax(x):
	shiftx = x - np.max(x)
	exps = np.exp(shiftx)
	return exps / np.sum(exps)
```
3.这时候计算稳定，但是输入的数值差过大也会报错，例如$[-1000，0，10000000]$ 会报NaN错误，一种解决方案就是使用LogSoftmax,也就是cross-entrop里实现的方法
$log(s_i)=log(\frac{e^{z_i}}{\sum_{j=1}^n {e^{z_j}}})=log(e^{zi})-log({\sum_{j=1}^n {e^{z_j}}})=a_i-log({\sum_{j=1}^n {e^{z_j}}})$





![enter description here](https://raw.githubusercontent.com/ZhaoKangkang0572/imgbed/master/小书匠/1598341626729.png)


![enter description here](https://raw.githubusercontent.com/ZhaoKangkang0572/imgbed/master/小书匠/1598345168673.png)


Reference:
https://www.zhihu.com/question/294679135/answer/885285177?utm_source=wechat_session&utm_medium=social&utm_oi=983381859228557312