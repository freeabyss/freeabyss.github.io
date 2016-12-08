---
title: Math-DM-05-推理规则
date: 2016-12-03 17:55:52
tags: [Discrete Mathematics, Math, note]
categories: [Math]
---
## 推理规则
证明是建立在数学命题真实性之上的有效论证。    
为从已有的命题中推出新的命题，应用推理规则，它是构造有效论证的模板。推理规则是建立命题真实性的基本工具。     

### 命题逻辑的推理规则
命理逻辑中的论证是一连串的命题。除了论证中最后一个命题外都叫前提，最后的命题叫结论。当所有前提为真意味着结论为真时，一个论证是有效的。     
表示命题逻辑论证有效的关键是表示出它的__论证形式__有效。    
我们可以先建立一些简单的论证形式，称为__推理规则__这些推理规则可以作为模板来构造更多复杂的有效论证形式。     

|推理规则|永真式|名称|
|:-----|:----|:---|
|$\begin{array}{cl} & p \\ & \underline {p\rightarrow q} \\ \therefore & q \\ \end{array}$| $[p\land(p\rightarrow q)]\rightarrow q$| 假言推理|
|$\begin{array}{cl} &\lnot p \\ & \underline {p\rightarrow q} \\ \therefore & \lnot p \\ \end{array}$|$[\lnot q\land (p\rightarrow q)]\rightarrow \lnot p$|取拒式|
|$\begin{array}{cl} & p\rightarrow q \\ & \underline {q\rightarrow r} \\ \therefore & p\rightarrow r \\ \end{array}$|$[(p\rightarrow q)\land (q\rightarrow r)]\rightarrow (p\rightarrow r)$|假言三段论|
|$\begin{array}{cl} & p\lor q \\ & \underline {\lnot p} \\ \therefore & q \\ \end{array}$|$[(p\lor q)\land \lnot p]\rightarrow q$|析取三段论|
|$\begin{array}{cl} & \underline p \\ \therefore & p\lor q \\ \end{array}$|$p\rightarrow (p\lor q)$| 附加|
|$\begin{array}{cl} &\underline {p\land q} \\\therefore & p\\ \end{array}$|$(p\land q)\rightarrow p$|化简|
|$\begin{array}{cl} & p \\ & \underline q \\ \therefore & p\land q \\ \end{array}$|$(p\land q)\rightarrow (p\land q)$|合取|
|$\begin{array}{cl} & p\lor q \\ & \underline {\lnot p\lor r} \\ \therefore & q\lor r \\ \end{array}$|$[(p\lor q)\land (\lnot p\lor r)]\rightarrow (q\lor r)$|消解|

### 量词命题的推理规则

|推理规则|名称|
|:-----|:---|
|$\begin{array}{cl} & \underline {\forall xP(x)} \\ \therefore & P(c) \\ \end{array}$| 全称示例|
|$\begin{array}{cl} & \underline {P(x),任意c} \\ \therefore & \forall xP(x)\\ \end{array}$ |全称生成|
|$\begin{array}{cl} & \underline {\exists P(x)} \\ \therefore & P(c),对某个元素\\ \end{array}$|存在示例|
|$\begin{array}{cl} & \underline {P(c),对某个元素} \\ \therefore & \exists xP(x)\\ \end{array}$|存在生成|
|$\begin{array}{cl} & \forall x(P(x)\rightarrow Q(x)) \\ & \underline {P(a), 其中a是论域中一个特定的元素} \\ \therefore & Q(a) \\ \end{array}$|全称假言推理|

### 命题逻辑推理规则和量化语句的推理规则结合
|推理规则|名称|
|:-----|:---|
|$\begin{array}{cl} & \forall x(P(x)\rightarrow Q(x)) \\ & \underline {P(a), 其中a是论域中一个特定的元素} \\ \therefore & Q(a) \\ \end{array}$|全称假言推理|
|$\begin{array}{cl} & \forall x(P(x)\rightarrow Q(x)) \\ & \underline {\lnot Q(a), 其中a是论域中一个特定的元素} \\ \therefore & \lnot P(a) \\ \end{array}$|全称取拒推理|
|$\begin{array}{cl} & \forall x(P(x)\rightarrow Q(x)) \\ & \underline {\forall x(Q(x)\rightarrow R(x))} \\ \therefore & \forall x(P(x)\rightarrow R(x)) \\ \end{array}$|全称传递性|


