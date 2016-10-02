---
title: 行列式－《线性代数及应用》
date: 2016-09-08 20:44:04
updated: 2016-09-10 20:00:00
tags: [Math, Linear Algebra, note]
categories: Math
---
> 加粗小写字母代表向量，例如$\mathbf u, \mathbf v$    
> 不加粗小写字母代表标量也就是实数，例如$a,c$   
> 大写字母代表矩阵，例如 $A,B$

## 定义
当$n\ge 2$时，$n\times n$矩阵$A=[a_{ij}]$的行列式是形如$\pm a_{1j}detA_{1j}$的$n$个项的和，其中加号和减号交替出现，这里元素$a_{11},a_{12},\cdots,a_{1n}$来自$A$的第一行，即
$$
    detA=a_{11}\cdot detA_{11}-a_{12}\cdot detA_{12}+\cdots+(-1)^{1+n}a_{1n}\cdot detA_{1n} \\
    = \sum_{j=1}^n (-1)^{1+j}a_{1j}detA_{1j}
$$
其中，$A_{ij}$表示通过划去$A$中第$i$行和第$j$列而得到的子矩阵。

## 性质
### 行列式函数
若$A$为$n\times n$矩阵，我们可以将$detA$看作$A$中$n$个列向量的函数。如果将$A$其中一列作为可变列，则$detA$可作为可变列向量的线性函数。
$$
    A=[\mathbf a_1 \cdots \mathbf a_{j-1} \mathbf x  \mathbf a_{j+1} \cdots \mathbf a_n]
$$
定义由$R^n$到$R$的变化T为
$$
    T(\mathbf x) = det[[\mathbf a_1 \cdots \mathbf a_{j-1} \mathbf x \mathbf a_{j+1} \cdots \mathbf a_n]]
$$
则有有以下性质
$$
    T(c\mathbf x) = cT(\mathbf x), 对任意常数c和R^n中的任意\mathbf x成立 \\
    T(\mathbf u+\mathbf v)=T(\mathbf u)+T(\mathbf v), 对R^n中所有\mathbf u,\mathbf v成立
$$

## 定理
1. $n\times n$矩阵$A$的行列式可按任意行或列的余因子展开式来计算。    
按第$i$行展开
$$
    C_{ij} = (-1)^{i+j}detA_{ij} \\
    detA = a_{i1}C_{i1}+a_{i2}C_{i2}+\cdots+a_{in}C_{in}
$$
按第$j$列展开
$$
    C_{ij} = (-1)^{i+j}detA_{ij} \\
    detA = a_{1j}C_{1j}+a_{2j}C_{2j}+\cdots+a_{nj}C_{nj}
$$
2. 若$A$为三角阵，则$detA$等于$A$的主对角线上元素的乘积
3. 行变换，令$A$是一个方阵
    * 若$A$的某一行的倍数加到另一行得矩阵$B$，则$detB=detA$
    * 若$A$的两行互换得矩阵$B$，则$detB=-detA$
    * 若$A$的某行乘以$k$倍得到矩阵$B$，则$detB=k\cdot detA$
4. 方阵$A$是可逆的当且仅当$detA\neq 0$
5. 若$A$为一个$n\times n$矩阵，则$detA^T = detA$
6. 若$A$和$B$均为$n\times n$矩阵，则$detAB = (detA)(detB)$
7. 克拉默法则，设$A$是一个可逆的$n\times n$矩阵，对$R^n$中任意向量$\mathbf b$，方程$A\mathbf x=\mathbf b$的唯一解可由下式给出，其中$detA_i(\mathbf b)$表示$A$中第$i$列由向量$\mathbf b$替换得到的矩阵
$$
    x_i = {detA_i(\mathbf b)\over {detA}}, i=1,2,\cdots,n
$$
8. 逆矩阵公式， 设$A$是一个可逆的$n\times n$矩阵，则$A^{-1}={1\over detA}adjA$
9. 若$A$是一个$2\times 2$矩阵，则由$A$的列确定的平行四边形的面积为$|detA|$，若$A$是一个$3\times 3$矩阵，则由$A$列确定的平行六面体的体积为$|detA|$
10. 设$T:R^2\to R^2$是由一个$2\times 2$矩阵$A$确定的线性变换，若$S$是$R^2$中一个平行四边形，则
$$
    \{T(S)的面积\}=|detA|\cdot\{S的面积\} 
$$
若$T$是一个由$3\times 3$矩阵$A$确定的线性变换，而$S$是$R^3$中的一个平行六面体，则
$$
    \{T(S)的体积\}=|detA|\cdot \{S的体积\}
$$

## 推论
### $adjA$可逆
若$A$可逆，则$adjA$也可逆，且$(adjA)^{-1}={1\over detA}A$
$$
    A^{-1} = {1\over detA}adjA \\
    adjA = (detA)A^{-1} \\
    adjA(adjA)^{-1} = I \\
    adjA \cdot {1\over detA}A = I \\
    (detA)A^{-1} \cdot {1\over detA}A = I \\
    A^{-1}A = I
$$







