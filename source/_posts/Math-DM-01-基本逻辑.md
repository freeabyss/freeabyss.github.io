---
title: Math-DM-01-基本逻辑
date: 2016-11-26 16:33:43
updated: 2016-11-28 22:58:00
tags: [Discrete Mathematics, Math, note]
categories: [Math]
---
## 命题逻辑
逻辑的基本成分是命题，命题是一个或真或假的陈述语句，即一个陈述事实的句子，但不能既真又假。    
涉及命题的逻辑领域称为命题演算或命题逻辑。

## 逻辑运算符
### 非
令$p$为一命题，则$p$的否定表示为$\lnot p$，命题$\lnot p$读作"非$p$"。
### 与(合取)
令$p$和$q$为命题，$p、q$的合取用$p\land q$表示。即命题$p$并且$q$。
### 或(析取)
令$p$和$q$为命题，$p、q$的析取用$p\lor q$表示。即命题$p$或$q$。
### 异或
令$p$和$q$为命题。$p$和$q$的异或是一个命题。当$p$和$q$($p\oplus q$)中只有一个为真时命题为真，否则为假。
### 与非
命题$p NAND q$(也记作$p\vert q$)在$p$和$q$均为真时为假，否则为真。
### 或非
命题$p NOR q $(也记作$p\downarrow q$)在$p$和$q$均为假时为真，否则为假。
### 条件语句
令$p$和$q$为命题，条件语句$p\rightarrow q$ 是命题“若$p$，则$q$”。    当$p$为真而$q$为假时，条件语句$p\rightarrow q$为假，否则为真。   
在条件语句$p\rightarrow q$中，$p$称为假设、前提，$q$称为结论。    
条件语句也称蕴含。

#### 逆、倒置和反
命题$q\rightarrow p$称为$p\rightarrow q$的逆蕴含。    
命题$\lnot q\rightarrow \lnot p$称为$p\rightarrow q$的倒置蕴含。   
命题$\lnot p\rightarrow \lnot q$称为$p\rightarrow q$的反蕴含。  

### 双条件语句
令$p$和$q$为命题。双条件语句$p↔︎q$是命题“$p$当且仅当$q$”。当$p$和$q$有相同真值时，双条件语句为真，否则为假。    
双条件语句也称双蕴含。  

### 真值表

|p <span style="margin-left:20px">q</span>| $\lnot p$| $p\land q$|$p\lor q$|$p\oplus q$|$p\rightarrow q$|$p↔︎q$|$p \vert q$|$p\downarrow q$|
|:----:|:--------:|:---------:|:-------:|:---------:|:------:|:---:|:--:|:--:|
|T <span style="margin-left:20px">T</span>| F|T|T|F|T|T|F|F|
|T <span style="margin-left:20px">F</span>| F|F|T|T|F|F|T|F|
|F <span style="margin-left:20px">T</span>| T|F|T|T|T|F|T|F|
|F <span style="margin-left:20px">F</span>| F|F|F|F|T|T|T|T|

### 逻辑运算符的优先级
* 否定运算符在其他所有逻辑运算符之前执行。
* 合取运算优先于析取运算。
* 条件运算和双条件运算优先级低于合取和析取运算。

