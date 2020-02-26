---
title: 二进制运算
date: 2016-12-22 22:52:26
tags: [Math,function,Alg]
categories: [Math]
---

## 整数相加
$$
\begin{array}{l}
\mathbf {procedure} \; \mathcal {add} (a, b:integer)\\  
\{a和b的二进制展开分别是(a_{n-1}a_{n-2}\dots a_1a_0)_2和(b_{n-1}b_{n-2}\dots b_1b_0)_2\} \\
c:= 0  \\
\mathbf {for}\; j:=0 \;\mathbf {to}\; n-1 \\
\mathbf {begin} \\
\qquad d:=\lfloor (a_j+b_j+c)/2\rfloor \\
\qquad s_j:=a_j+b_j+c-2d \\
\qquad c:=d \\
\mathbf {end}  \\
s_n := c \\
\{和数的二进制展开是(s_ns_{n-1}\dots s_0)_2\} 
\end{array}
$$
## 整数相乘
$$
\begin{array}{l}
\mathbf {procedure} \;\mathcal {multiply} (a, b:integer)\\  
\{a和b的二进制展开分别是(a_{n-1}a_{n-2}\dots a_1a_0)_2和(b_{n-1}b_{n-2}\dots b_1b_0)_2\} \\
\mathbf {for}\; j:=0 \;\mathbf {to}\; n-1 \\
\mathbf {begin} \\
\qquad \mathbf {if}\; b_j=1\;\mathbf {then}\; c_j:=a\;shifted\; j places \\
\qquad \mathbf{else}\; c_j:=0\\
\mathbf {end} \\
\{c_0,c_1,\dots,c_{n-1}是部分乘积\} \\
p:=0\\
\mathbf {for}\; j:=0\;\mathbf {to}\; n-1 \\
\qquad p:=p+c_j \\
\{p是ab的值\}
\end{array}
$$
