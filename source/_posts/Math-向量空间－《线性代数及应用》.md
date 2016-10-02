---
title: 向量空间－《线性代数及应用》
date: 2016-09-10 20:02:45
tags: [Math, Linear Algebra, note]
categories: Math
---
> 加粗小写字母代表向量，例如$\mathbf u, \mathbf v$    
> 不加粗小写字母代表标量也就是实数，例如$a,c$   

## 向量空间和子空间
### 向量空间
一个向量空间是由一些被称为向量的对象构成的非空集合$V$，在这个集合上定义两个运算，称为加法和标量乘法，服从以下公理，这些公理必须对$V$中所有向量$\mathbf u,\mathbf v,\mathbf w$及所有标量$c,d$均成立。

* $\mathbf u, \mathbf v$之和表示为$\mathbf u+\mathbf v$，仍在$V$中
* $V$中存在一个零向量$0$，使得$\mathbf u+0=\mathbf u$
* 对$V$中每个向量$\mathbf u$，存在$V$中向量$-\mathbf u$，使得$\mathbf u+(-\mathbf u)=0$
* $\mathbf u$与标量$c$的标量乘法记为，$c\mathbf u$，仍在$V$中
$$
    \mathbf u+\mathbf v ＝ \mathbf v+\mathbf u \\
    (\mathbf u+\mathbf v)+\mathbf w=\mathbf u+(\mathbf v+\mathbf w) \\
    c(\mathbf u+\mathbf v)=c\mathbf u+c\mathbf v \\
    (c+d)\mathbf u=c\mathbf u+d\mathbf u \\
    c(d\mathbf u)=(cd)\mathbf u \\
    1\mathbf u=\mathbf u  \\
    0\mathbf u=0 \\
    c0=0 \\
    -\mathbf u=(-1)\mathbf u\\
$$

## 零空间、列空间和线性变换
### 零空间
$m\times n$矩阵$A$的零空间写成$NulA$，是齐次方程$A\mathbf x=0$的全体解的集合，用集合符号表示即：
$$
    NulA = {\mathbf x:\mathbf x \in \mathbb R^n, A\mathbf x =0}
$$
$NulA$可以进一步的描述为$\mathbb R^n$中在线性变换$\mathbf x \mapsto A\mathbf x$下映射到$\mathbb R^m$中的零向量的全体向量的集合。

求矩阵$A$的零空间生成集的过程，就是解方程$A\mathbf x=0$的过程。
>* 由该方法产生的生成集必然是线性无关的。
>* 生成集中向量的个数等于方程$A\mathbx x=0$中自由变量的个数


### 子空间
向量空间$V$的一个子空间是$V$的一个满足以下三个性质的子集$H$：

* $V$中的零向量在$H$中
* $H$对向量加法封闭，即对$H$中任意向量$\mathbf u,\mathbf v$，和$\mathbf u+\mathbf v$仍在$H$中
* $H$对标量乘法封闭，即对$H$中任意向量$\mathbf u$和任意标量$c$，向量$c\mathbf u$仍在$H$中

### 矩阵的列空间
$m\times n$矩阵的列空间(记为$ColA$)是由$A$的列的所有线性组合组成的集合，若$A=[\mathbf a_1,\cdots,\mathbf a_n]$，则$ColA = Span\{\mathbf a_1,\cdots,\mathbf a_n\}$    
$ColA$)可写成$A\mathbf x$的形式，其中$\mathbf x$为某向量，$A\mathbf x$表示$A$的列向量的一个线性组合，即
$$
    ColA = {\mathbf b:\mathbf b = A\mathbf x, \mathbf x \in \mathbb R^n}
$$
$m\times n$矩阵的列空间等于$\mathbb R^m$当且仅当方程$A\mathbf x=\mathbf b$对$\mathbb R^m$中每个$\mathbf b$有解

### $NulA$与$ColA$的对比
对于$m\times n$矩阵$A$，$NulA$与$ColA$之间的对比

|$NulA$|$ColA$|
|:-----|:-----|
|$NulA$是$\mathbb R^n$的一个子空间|$ColA$是$\mathbb R^m$的子空间|
|$NulA$是隐式定义的，即仅给出了一个$NulA$中向量必须满足的条件($A\mathbf x=0$)|$ColA$是显式定义，即明确指出如何建立$ColA$中的向量|
|求$NulA$中的向量需要对$[A 0]$做行变换|$A$中的列就是$ColA$的向量，其余的可由$A$的列表示出来|
|$NulA$与$A$的数值之间没有明显的关系|$ColA$与$A$的数值由明显的关系，因为$A$的列就在$ColA$中|
|$NulA$的一个典型向量$\mathbf v$具有$A\mathbf v=0$的特质|$ColA$中一个典型的向量$v$具有方程$A\mathbf x=\mathbf v$是相容的性质|
|给一个特定的向量$\mathbf v$，容易判断$\mathbf v$是否在$NulA$中，仅需计算$A\mathbf v$|给一个特定的向量$\mathbf v$，判断$\mathbf v$是否在$ColA$中，需对$[A \mathbf v]$作行变换|
|$NulA ={0}$ 当且仅当方程$A\mathbf x=0$仅有平凡解|$ColA =\mathbb R^m$当且仅当方程$A\mathbf x=\mathbf b$对每一个$\mathbf b \in \mathbb R^m$有一个解|
|$NulA ={0}$ 当且仅当线性变换$\mathbf x\mapsto A\mathbf x$是一对一的|$ColA =\mathbb R^m$当且仅当线性变换$\mathbf x\mapsto A\mathbf x$将$\mathbb R^n$映射到$\mathbb R^m$|

### 线性变换的核与值域
由向量空间$V$映射到向量空间$W$内的线性变换$T$是一个规则，它将$V$中每个向量$\mathbf x$映射城$W$中惟一向量$T(\mathbf x)$，且满足
$$
    T(\mathbf u+\mathbf v) = T(\mathbf u)+T(\mathbf v), 对V中所有\mathbf u,\mathbf v 均成立 \\
    T(c\mathbf u) = cT(\mathbf u),对V中所有\mathbf u及所有数c均成立
$$
线性变换$T$的*核*(或称零空间)是$V$中所有满足$T(\mathbf u)=0$的向量$\mathbf u$的集合。   
$T$的*值域*是$W$中所有具有形式$T(\mathbf x)$的向量的集合。      
如果$T$是由一个矩阵变换得到的，例如$T(\mathbf x)=A\mathbf x$，则$T$的核与值域对应$A$的零空间和列空间。 

## 线性无关集和基
### 线性无关集
$V$中向量的一个指标集$\{\mathbf v_1,\cdots,\mathbf v_p\}$，称为线性无关的，如果向量方程
$$
    c_1\mathbf v_1+c_2\mathbf v_2+\cdots+c_p\mathbf v_p = 0
$$
只有平凡解。
*矩阵的行初等变换不影响矩阵的列的线性相关关系*

### 基
令$H$是向量空间$V$的一个子空间，$V$中向量的指标集$B＝\{\mathbf b_1,\cdots,\mathbf b_p\}$称为$H$的一个基，如果
* $B$是现象无关集
* 由$B$生成的子空间与$H$相同，即$H=Span\{\mathbf b_1,\cdots,\mathbf b_p\}$

#### 基的两个特性
> * 基是一个尽可能小的生成集
> * 基是尽可能大的线性无关集

### $NulA$和$ColA$的基
通过解$A\mathbf x=0$的出的生成集总是线性无关的，即$NulA$的基。     
$ColA$的基由矩阵$A$的主元列构成。


## 定理
1. 若$\mathbf v_1,\cdots,\mathbf v_p$在向量空间$V$中，则$Span\{\mathbf v_1,\cdots,\mathbf v_p\}$是$V$的一个子空间
2. $m\times n$矩阵$A$的零空间是$\mathbb R^n$的一个子空间，也就是说，$m$个方程、$n$个未知数的齐次线性方程组$A\mathbf x=0$的全体解的集合是$\mathbb R^n$的一个子空间。
3. $m\times n$矩阵$A$的列空间是$\mathbb R^m$的一个子空间
4. 不少于两个有编号的向量的集合$\{\mathbf v_1,\cdots,\mathbf v_p\}$，如果有$\mathbf v_1 \neq0$，则$\{\mathbf v_1,\cdots,\mathbf v_p\}$是线性相关的，当且仅当某$\mathbf v_1(j>1)$是其前面向量$v_1,\cdots,v_{j-1}$的线性组合
5. 生成集定理: 令$S=\{\mathbf v_1,\cdots,\mathbf v_p\}$是$V$中的向量集，$H=Span\{\mathbf v_1,\cdots,\mathbf v_p\}$.
    * 若$S$中某一向量，比如说$v_k$，是$S$中其余向量的线性组合，则$S$中去掉$v_k$之后形成的集合仍然可以生成$H$。
    * 若$H\neq\{0\}$，则$S$的某一子集是$H$的一个基
6.矩阵$A$的主元列构成$ColA$的一个基




