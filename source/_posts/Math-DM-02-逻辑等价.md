---
title: Math-DM-02-逻辑等价
date: 2016-11-26 16:58:58
tags: [Discrete Mathematics, Math, note]
categories: [Math]
---
## 引言
复合命题中如果无论其中出现的命题的真值是什么，它的真值总是真，称为永真式。真值永远为假的复合命题称为矛盾。最后，既不是永真式又不是矛盾的命题称为可能式。

### 逻辑等价
在所有可能的情况下都有相同真值的两个复合命题称为逻辑等价。用如下定义这一概念：  

* 如果$p↔︎q$是永真式。命题$p$和$q$称为逻辑等价的。记作$p\equiv q$，有时也记作$p⇔q$。
> 符号$\equiv$不是逻辑链接符，因为$p\equiv q$不是复合命题。

## 摩根定律及应用
$\mathbf T$表示永远为真的复合命题，$\mathbf F$表示永远为假的复合命题。

|名称 | 等价关系|
|:---|:-------|
|摩根定律|$\lnot (p\land q) \equiv \lnot p \lor \lnot q$ <br> $\lnot (p\lor q) \equiv \lnot p \land \lnot q$ |
|恒等律|$p\land \mathbf T \equiv p$ <br> $p\lor \mathbf F \equiv p$|
|支配律|$p\lor \mathbf T \equiv \mathbf T$ <br> $p\land \mathbf F \equiv \mathbf F$|
|幂等律|$p\land p \equiv p$ <br> $p\lor p \equiv p$|
|双非律|$\lnot(\lnot p) \equiv p$|
|交换律|$p\lor q \equiv q\lor p$ <br> $p\land q\equiv q\land p$|
|结合律|$(p\lor q)\lor r\equiv p\lor (q\lor r)$ <br> $(p\land q)\land r\equiv p\land (q\land r)$|
|分配律|$p\lor(q\land r) \equiv (p\lor q)\land (p\lor r)$ <br> $p\land (q\lor r) \equiv (p\land q)\lor (p\land r)$|
|吸收律|$p\lor (p\land q)\equiv p$ <br> $p\land (p\lor q)\equiv p$|
|否定律|$p\lor \lnot p\equiv \mathbf T$<br> $p\land \lnot p\equiv \mathbf F$|

### 涉及条件语句的逻辑等价
$$
p\rightarrow q\equiv \lnot p\lor q \\
p\rightarrow q\equiv \lnot q\rightarrow \lnot p \\
p\lor q\equiv \lnot p\rightarrow q\\
p\land q\equiv \lnot(p\rightarrow \lnot q) \\
\lnot(p\rightarrow q)\equiv p\land \lnot q\\
(p\rightarrow q)\land (p\rightarrow r)\equiv p\rightarrow (q\land r)\\
(p\rightarrow r)\land (q\rightarrow r)\equiv (p\lor q)\rightarrow r\\
(p\rightarrow q)\lor (p\rightarrow r)\equiv p\rightarrow (q\lor r)\\
(p\rightarrow r)\lor (q\rightarrow r)\equiv (p\land q)\rightarrow r\\
$$

### 涉及双条件语句的逻辑等价
$$
p↔︎q \equiv (p\rightarrow q)\land (q\rightarrow p)\\
p↔︎q \equiv \lnot p↔︎ \lnot q \\
p↔︎q \equiv (p \land q)\lor (\lnot p\land \lnot q)\\
\lnot (p↔︎q) \equiv p↔︎\lnot q
$$