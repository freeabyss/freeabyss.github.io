---
title: 集合-函数-数列
date: 2016-10-02 22:32:10
updated: 2016-10-05 9:10:00
tags: [Discrete Mathematics, Math, note]
categories: [Math]
---
## 集合
### 集合概述
* 集合$A$等于集合$B$当且仅当$∀x(x\in A↔︎x\in B)$
* 集合$A$是集合$B$的子集当且仅当$∀x(x\in A→x\in B)$
* 集合$A$是集合$B$的真子集当且仅当$∀x(x\in A→x\in B)∧∃x(x∈B∧x∉A)$
* 幂集合：幂集合是集合$S$所有子集的集合，包含空集合集合$S$本身，用$P(S)$表示
    - 如果集合有$n$个元素，那么幂集合的个数为$2^n$个
* 有序$n$元祖，是由$n$个元素构成的有序组。
* 笛卡儿积：集合$A_1,A_2,\dots,A_n$的笛卡儿积用$A_1\times A_2\times \dots \times A_n$表示，这是有序$n$元组$(a_1,a_2,\dots,a_n)$的集合，其中对于$i=1,2,\dots,n, a_i∈A$
$$
    A_1\times A_2\times \dots \times A_n = {(a_1,a_2,\dots ,a_n)|a_i∈A,i=1,2,\dots,n}
$$
* $∀x∈S(P(x))$是$∀x(x∈S→P(x))$的简写
* $∃x∈S(P(x))$是$∃x(x∈S∧P(x))$的简写

### 集合运算
* 并集：$A\cup B=\{x\mid x\in A∨x\in B\}$
* 交集：$A\cap B=\{x\mid x\in A∧x\in B\}$
* 如果两集合的交集为空集，就说它们不相交
* 差集：$A$与$B$的差集也称$B$对于$A$的补集，$A-B=\{x\mid x\in A∧x\notin B\}$
* 令$U$为全集，集合$A$的补集用$\bar A$表示，这是$A$对$U$的补集，$\bar A=\{x\mid x\notin A\}$

#### 集合恒等式
|等式|名称|
|:--|:--|
|$A∪\varnothing=A$ <br>$A\cap U=A$|恒等律|
|$A\cup U=U$<br>$A\cap \varnothing=\varnothing$|支配律|
|$A\cup A=A$<br>$A\cap A=A$|幂等律|
|$\overline {(\bar A)}=A$|补集律|
|$A\cup B=B\cup A$<br>$A\cap B=B\cap A$|交换律|
|$A\cup (B\cup C)=(A\cup B)\cup C$<br>$A\cap(B\cap C)=(A\cap B)\cap C$|结合律|
|$A\cup(B\cap C)=(A\cup B)\cap(A\cup C)$<br>$A\cap(B\cup C)=(A\cap B)\cup(A\cap C)$|分配律|
|$\overline{A\cup B}=\bar A\cap \bar B$<br>$\overline{A\cap B}=\bar A\cup \bar B$|德摩根定律|
|$A\cup(A\cap B)=A$<br>$A\cap(A\cup B)=A$|吸收律|
|$A\cup \bar A=U$<br>$A\cap \bar A=\varnothing$|补集|

#### 扩展的交集和并集
* 一组集合的并集是包含哪些至少是这组集合中一个集合成员的元素的集合  
$$
    A_1\cup A_2\cup \cdots\cup A_n=\underset{i=1}{\overset{n}\bigcup}A_i
$$
* 一组集合的交集是包含哪些属于这组集合中所有成员集合的元素的集合
$$
    A_i\cap A_2\cap \cdots\cap A_n=\underset{i=1}{\overset{n}\bigcap}A_i
$$

## 函数
### 几个重要的函数
* 下取整函数：把$x$下舍入到小于或等于$x$又最接近$x$的整数，$x$的值用$⎡x⎤$表示
* 上取整函数：把$x$上舍入到大于或等于$x$又最接近$x$的整数，$x$的值用$⎣x⎦$表示
* 下取整函数又称最大整数函数，又用$［x］$表示

#### 下取整函数和上取整函数性质
> n 表示整数

* $⎣x⎦=n $当且仅当$n\le x\lt n+1$
* $⎣x⎦=n $当且仅当$x-1\lt n\le x$
* $⎡x⎤=n $当且仅当$n-1\lt x\le n$
* $⎡x⎤=n $当且仅当$x\le n\lt x+1$
* $x-1\lt ⎣x⎦\le x\le ⎡x⎤\lt x+1$
* $⎣-x⎦=-⎡x⎤$
* $⎡x⎤=-⎣-x⎦$
* $⎣x+n⎦=⎣x⎦+n$
* $⎡x+n⎤=⎡x⎤+n$

## 序列
* 序列：序列是从整数集合的子集(通常是$\{0,1,2,\dots \}$或$\{1,2,3,\dots \}$)到集合$S$的函数。用记号$a_n$表示整数$n$的像，称$a_n$为序列的一个项。
* 有穷序列也被称作串，空串用$\lambda$表示。
* 几何序列：是如下形式的序列，即指数函数$f(x)=ar^x$离散对应物，初项$a$和公比$r$都是实数。
$$
a, ar, ar^2, \cdots ,ar^n, \cdots
$$
* 等差数列：是如下形式的序列，即线性函数$f(x)=dx+a$的离散对应物，初项$a$和公差$d$都是实数。
$$
    a, a+d, a+2d, \cdots , a+nd, \cdots
$$

### 找出序列规则的技巧
* 是否有相同的值连续出现
* 是否给前项加上常量或者与序列中位置相关的量就得到后项
* 是否给前项乘以特定的量就能得到后项
* 是否按照某种方式组合前项就能得到后项
* 是否各项之间存在某种循环

### 序列求和公式
#### 几何序列求和
$$\sum_{j=0}^n ar^j = \begin{cases}
{ar^{n+1}-a\over {r-1}} 若r\neq 1 \\[2ex]
(n+1)a 若 r=1
\end{cases}
$$

#### 其他求和公式
|和|闭形式|和|闭形式|
|:-|:---|:-|:----|
|$$\sum_{k=0}^n ar^k(r\neq 0)$$|$${ar^{n+1}-a\over r-1},r\neq 1$$|$$\sum_{k=1}^n k^3$$|$$n^2(n+1)^2\over 4$$|
|$$\sum_{k=1}^n k$$|$$n(n+1)\over 2$$|$$\sum_{k=0}^\infty x^k, \mid x\mid\lt 1$$|$$1\over 1-x$$|
|$$\sum_{k=1}^n k^2$$|$$n(n+1)(2n+1)\over 6$$|$$\sum_{k=1}^\infty kx^{k-1}, \mid x\mid\lt 1$$|$$1\over (1-x)^2$$|

### 基数
* 集合$A$与集合$B$有相同的基数，当且仅当存在从$A$到$B$的一一对应
* 有限集或与自然数集基数相同的无限集称为可数的，反之称为不可数的。
* 如果无穷集合$S$是可数的，我们用符号$\aleph_0$来表示集合$S$的基数。记作$\mid S\mid=\aleph_0$，且说$S$有基数希伯来零。





