---
title: Math-DM-04-嵌套量词
date: 2016-12-03 10:51:05
tags: [Discrete Mathematics, Math, note]
categories: [Math]
---
## 嵌套量词
嵌套量词类似于复合函数，例如$\forall x\exists y(x+y=0)$和$\forall xQ(x)$相同，其中$Q(x)$指$\exists y(x+y=0)$。

### 嵌套量词例子
这里假定$x$和$y$的论域是所有实数的集合。 
$$ \forall x\forall y(x+y=y+x)$$
对于所有实数$x$和$y$，$x+y=y+x$。这是实数加法的交换律。
$$\forall x\exists y(x+y=0) $$
对于所有实数$x$，存在一个实数$y$，使得$x+y=0$。
$$\forall x\forall y\forall z(x+(y+z)=(x+y)+z)$$

### 嵌套顺序
除非所有的量词均为全称量词或存在量词，否则量词的顺序不同会导致不同的真值。

|语句|何时为真 |何时为假|
|:--|:------|:------|
|$\forall x\forall yP(x,y)$<br> $\forall y\forall xP(x,y)$|对每一对$x、y$，$P(x,y)$均为真|有一对$x、y$使$P(x,y)$为假|
|$\forall x\exists yP(x,y)$|对每个$x$，都有$y$使$P(x,y)$为真|有$x$，使$P(x,y)$对每个$y$总是假|
|$\exists x\forall yP(x,y)$|有一个$x$，使所有$y$对$P(x,y)$均为真|对每个$x$都有$y$使$P(x,y)$为假|
|$\exists x\exists yP(x,y)$<br> $\exists y\exists xP(x,y)$|有一对$x、y$，$P(x,y)$为真|对每一对$x、y$，$P(x,y)$均为假|

### 将数学语句翻译成涉及嵌套量词的语句
1、两个正整数的和是整数
$$ \forall x\forall y((x>0)\land(y>0)\rightarrow (x+y>0))$$
2、每个实数(除$0$外)都有乘法逆元
$$ \forall x((x\neq 0)\rightarrow \exists y(xy=1))$$

