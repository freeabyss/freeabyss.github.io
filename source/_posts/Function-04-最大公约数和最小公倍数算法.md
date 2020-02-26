---
title: 最大公约数和最小公倍数算法
date: 2016-12-22 21:28:03
tags: [Math,function,Alg]
categories: [Math]
---

## 因数分解
### 最大公约数
假定两个不全为$0$的整数$a$和$b$的素因子分解为：
$$
a=p_1^{a_1}p_2^{a_2}\dots p_n^{a_n} \\
b=p_1^{b_1}p_2^{b_2}\dots p_n^{b_n}
$$
每个整数都是非负整数，而且出现在$a$和$b$分解中的所有素数都包含在两个分解之中，必要时以0为指数出现。于是$gcd(a, b)$由下面的公式给出
$$
gcd(a, b) = p_1^{min(a_1,b_1)}p_2^{min(a_2, b_2)}\dots p_n^{min(a_n,b_n)}
$$
例如，求$120$和$500$的最大公约数：
$$
    120 = 2^3\cdot 3\cdot 5 , 500 = 2^2\cdot 5^3\\
    gcd(120, 500) = 2^{min(3,2)}\cdot 3^{min(1,0)}\cdot 5^{min(1,3)}\\
    = 2^3\cdot 3^0\cdot 5^1 = 20
$$

### 最小公倍数
因素分解也可以用来求最大公倍数，求$a$和$b$的最小公倍数的公式为:    
$$lcm(a, b) = p_1^{max(a_1,b_1)}p_2^{max(a_2, b_2)}\dots p_n^{max(a_n,b_n)}$$

## 欧几里得算法
欧几里德算法又称辗转相除法，用于计算两个整数 a,b 的最大公约数。其计算原理依赖于下面的定理：     
定理：$gcd(a,b) = gcd(b,a\;\mathbf{mod}\; b)$            
证明：$a$可以表示成$a = kb + r$，则 $r = a\;\mathbf{mod}\;b$     
假设$\;d$是$a$,$b$的一个公约数，则有$d\mid a$, $d\mid b$，而$r= a - kb$，因此 $d\mid r$       
因此$\;d$ 是$(b,a\;\mathbf{mod}\; b)$的公约数      
假设$\;d$是$(b,a\;\mathbf{mod}\;b)$ 的公约数，则$d\mid b$ ,$d\mid r$ ，但是$a = kb +r$      
因此$\;d$也是$(a,b)$的公约数
