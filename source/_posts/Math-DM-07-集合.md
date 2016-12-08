---
title: Math-DM-07-集合
date: 2016-12-08 12:37:07
tags: [Discrete Mathematics, Math, note]
categories: [Math]
---
## 集合
集合是一组无序的对象。
> 该定义有逻辑悖论。以公理的基本假设为起点建立集合理论可以避免逻辑上的不一致。
    
### 集合概述
* 集合$A$等于集合$B$当且仅当$∀x(x\in A↔︎x\in B)$
* 集合$A$是集合$B$的子集当且仅当$∀x(x\in A→x\in B)$
* 集合$A$是集合$B$的真子集当且仅当$∀x(x\in A→x\in B)∧∃x(x∈B∧x∉A)$
* 幂集合：幂集合是集合$S$所有子集的集合，包含空集合集合$S$本身，用$P(S)$表示
    - 如果集合有$n$个元素，那么幂集合的个数为$2^n$个

#### 笛卡儿积
##### 元组

有序$n$元组，是由$n$个元素构成的有序组，用括号表示：$(a_1,a_2,a_3,...,a_n)$。      
只有在两个有序$n$元组每一个对应的元素都相等时，它们才想等。二元组特称为有序偶。    
令$\mathbf A$和$\mathbf B$为集合，$\mathbf A$和$\mathbf B$的笛卡儿积用$\mathbf A\times\mathbf B$表示，是所有有序偶$(a,b)$的集合： 
$$ \mathbf A\times\mathbf B=\{(a,b)\mid a\in \mathbf A\land b\in \mathbf B\}$$

集合$A_1,A_2,\dots,A_n$的笛卡儿积用$A_1\times A_2\times \dots \times A_n$表示，这是有序$n$元组$(a_1,a_2,\dots,a_n)$的集合，其中对于$i=1,2,\dots,n, a_i∈A$
$$
    A_1\times A_2\times \dots \times A_n = \{(a_1,a_2,\dots ,a_n)\mid a_i∈A,i=1,2,\dots,n\}
$$
#### 带量词的集合符合
* $∀x∈S(P(x))$表示$P(x)$的全称量化，论域是集合$S$，等同于$∀x(x∈S→P(x))$。
* $∃x∈S(P(x))$表示$P(x)$的存在量化，论域是集合$S$, 等同于$∃x(x∈S∧P(x))$。

##### 实例
$\forall x\in \mathbf R(x^2\ge 0)$的含义是：任意实数的平方是非负的。      
$\exists x\in \mathbf Z(x^2=1)$的含义是：有某个整数的平方是1。

#### 量词的真值集合
我们把集合理论和谓词逻辑的概念结合起来，给定谓词$P$和论域$D$，定义$P$的真值集合:    
$D$中元素$x$使$P(x)$为真的元素组成的集合。$P(x)$的真值集合记为$\{x\in D\mid P(x)\}$。 
> 在域$\mathbf U$上，$\forall xP(x)$为真当且仅当$P$的真值集合是集合$U$。同样，域$U$上$\exists xP(x)$为真，当且仅当$P$的真值集合非空。


#### 常用集合表示
|符号|描述|
|:--|:---|
|$\mathbf Q$|有理数集|
|$\mathbf Q^+$| 正有理数集|
|$\mathbf N$|自然数集|
|$\mathbf Z$|整数集|
|$\mathbf Z^+$|正整数集|
|$\mathbf R$|实数集|
|$\varnothing$|空集|

> 注意，$\varnothing$不等于$\{\varnothing\}$

### 集合运算
|运算|描述|
|:--|:---|
|并集|$A\cup B=\{x\mid x\in A\lor x\in B\}$|
|交集|$A\cap B=\{x\mid x\in A\land x\in B\}$|
|差集|$A-B=\{x\in A\land x\notin B\}$|
|补集|$\overline A=\{x\mid x\in U\land x\notin A\}$|

> $U$为全集


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

##### 证明集合相等的方法
证明集合相等的一种方法是：证明两者中任何一个都是另一个的子集。    
另外一种方法是：证明一个元素如果属于第一个集合，必定属于第二个集合。 

##### 证明实例
$$ \begin{align}
\overline {A\cap B} &= \{x\mid x\notin A\cap B\} \\
&   =\{x\mid \lnot(x\in(A\cap B))\} \\
&   =\{x\mid \lnot(x\in A\land x\in B)\} \\
&   =\{x\mid \lnot (x\in A)\lor \lnot(x\in B)\}\\
&   =\{x\mid x\notin A\lor x\notin B\}\\
&   =\{x\mid x\in \overline{A}\lor x\in \overline{B}\} \\
&   =\{x\mid x\in \overline{A}\cup\overline{B}\} \\
&   =\overline{A}\cup\overline{B}
\end{align}
$$

#### 扩展的交集和并集
* 一组集合的并集是包含哪些至少是这组集合中一个集合成员的元素的集合  
$$
    A_1\cup A_2\cup \cdots\cup A_n=\underset{i=1}{\overset{n}\bigcup}A_i
$$
* 一组集合的交集是包含哪些属于这组集合中所有成员集合的元素的集合
$$
    A_i\cap A_2\cap \cdots\cap A_n=\underset{i=1}{\overset{n}\bigcap}A_i
$$
