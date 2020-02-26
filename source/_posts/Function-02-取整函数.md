---
title: 取整函数
date: 2016-12-14 20:41:20
tags: [Math,function,Alg]
categories: [Math]
---
## 上取整函数
上取整函数是指大于或等于实数$x$的最小整数，用$⎡x⎤$表示。

## 下取整函数
下取整函数是指小于或等于实数$x$的最大整数，用$⎣x⎦$表示。      
> 下取整函数也被称为最大整数函数，这时往往用$［x］$表示

## 性质
* $⎣x⎦=n $当且仅当$n\le x\lt n+1$
* $⎣x⎦=n $当且仅当$x-1\lt n\le x$
* $⎡x⎤=n $当且仅当$n-1\lt x\le n$
* $⎡x⎤=n $当且仅当$x\le n\lt x+1$
* $x-1\lt ⎣x⎦\le x\le ⎡x⎤\lt x+1$
* $⎣-x⎦=-⎡x⎤$
* $⎡x⎤=-⎣-x⎦$
* $⎣x+n⎦=⎣x⎦+n$
* $⎡x+n⎤=⎡x⎤+n$

> 在考虑下取整函数相关的语句时，一个有用的方法是令$x=n+\epsilon$，其中$n=⎣x⎦$是一个整数，$\epsilon$是$x$的分数部分，满足不等式$0\le\epsilon\lt 1$。 类似的考虑上取整函数时，通常写作$x=n-\epsilon$，其中$n=⎡x⎤$且$0\le\epsilon\lt 1$。

