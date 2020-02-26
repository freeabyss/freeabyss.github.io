---
title: MathJax tutorial
date: 2016-09-11 20:04:07
tags: [MathJax, markdown]
categories: MathJax
---
## 字符
### 希腊字母
|$\alpha$|$\beta$|$\gamma$|$\delta$|$\epsilon$|$\zeta$|$\eta$|$\theta$|
|:------:|:-----:|:------:|:------:|:--------:|:-----:|:----:|:------:|
|\alpha|\beta|\gamma|\delta|\epsilon|\zeta|\eta|\theta|
|$\iota$|$\kappa$|$\lambda$|$\mu$|$\nu$|$\xi$|$\omicron$|$\pi$|
|\iota|\kappa|\lambda|\mu|\nu|\xi|\omicron|\pi|
|$\rho$|$\sigma$|$\tau$|$\upsilon$|$\phi$|$\chi$|$\psi$|$\omega$|
|\rho|\sigma|\tau|\upsilon|\phi|\chi|\psi|\omega|

|$\Gamma$|$\Delta$|$\Theta$|$\Lambda$|$\Xi$|$\Pi$|$\Phi$|$\Psi$|
|:------:|:------:|:------:|:-------:|:---:|:---:|:----:|:----:|
|\Gamma|\Delta|\Theta|\Lambda|\Xi|\Pi|\Phi|\Psi|
|$\Sigma$|$\Upsilon$|$\Omega$|
|\Sigma|\Upsilon|\Omega|

### 运算符号

|$\lt$|$\gt$|$\le$|$\ge$|$\neq$|
|:---:|:---:|:---:|:---:|:----:|
|\lt|\gt|\le|\ge|\neq|

|$\times$|$\div$|$\pm$|$\mp$|$\cdot$|
|:---:|:---:|:---:|:---:|:---:|
|\times|\div|\pm|\mp|\cdot|

|$\cup$|$\cap$|$\setminus$|$\subset$|$\subseteq$|$\subsetneq$|
|:----:|:----:|:---------:|:-------:|:---------:|:----------:|
|\cup|\cap|\setminus|\subset|\subseteq|\subsetneq|
|$\supset$|$\in$|$\notin$|$\emptyset$|$\varnothing$|$\mid$|
|\supset|\in|\notin|\emptyset|\varnothing|\mid|

|$\to$|$\rightarrow$|$\leftarrow$|$\Rightarrow$|$\Leftarrow$|$\mapsto$|
|:---:|:---:|:---:|:---:|:---:|:---:|
|\to|\rightarrow|\leftarrow|\Rightarrow|\Leftarrow|\mapsto|

|$\land$|$\lor$|$\lnot$|$\forall$|$\exists$|$\top$|$\bot$|$\vdash$|$\vDash$|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|\land|\lor|\lnot|\forall|\exists|\top|\bot|\vdash|\vDash|

|$\star$|$\ast$|$\oplus$|$\circ$|$\bullet$|$\odot$|
|:-----:|:----:|:------:|:-----:|:-------:|:---:|
|\star|\ast|\oplus|\circ|\bullet|\odot|

|$\approx$|$\sim$|$\simeq$|$\cong$|$\equiv$|$\prec$|$\lhd$|
|:-------:|:----:|:------:|:-----:|:------:|:-----:|:----:|
|\approx|\sim|\simeq|\cong|\equiv|\prec|\lhd|

|$\infty$|$\aleph_0$|$\nabla$|$\partial$|$\Im$|$\Re$|
|:------:|:--------:|:------:|:--------:|:---:|:---:|
|\infty|\aleph_0|\nabla|\partial|\Im|\Re|

|$\ldots$|$\ell$|$\epsilon$|$\varepsilon$|$\varphi$|$\lceil x \rceil$|$\lfloor x \rfloor$|
|:------:|:----:|:--------:|:-----------:|:-------:|:----------------|:--|
|\ldots|\ell|\epsilon|\varepsilon|\varphi|\lceil x \rceil|\lfloor x \rfloor|


### 字体
* blackboard bold: \mathbb or\Bbb $\mathbb {ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnpqrstuvwxyz}$
* boldface: \mathbf $\mathbf {ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnpqrstuvwxyz}$
* typewriter: \mathtt $\mathtt {ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnpqrstuvwxyz}$
* roman font: \mathrm $\mathrm {ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnpqrstuvwxyz}$
* sans-serif font: \mathsf $\mathsf {ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnpqrstuvwxyz}$
* calligraphic: \mathcal $\mathcal {ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnpqrstuvwxyz}$
* script:\mathscr $\mathscr {ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnpqrstuvwxyz}$
* Fraktur:\mathfrak $\mathfrak {ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnpqrstuvwxyz}$

### 实例
`A_i\cap A_2\cap \cdots\cap A_n=\underset{i=1}{\overset{n}\bigcap}A_i`
$$A_i\cap A_2\cap \cdots\cap A_n=\underset{i=1}{\overset{n}\bigcap}A_i$$
`A_1\cup A_2\cup \cdots\cup A_n=\underset{i=1}{\overset{n}\bigcup}A_i`
$$A_1\cup A_2\cup \cdots\cup A_n=\underset{i=1}{\overset{n}\bigcup}A_i$$

```math
\begin{align}
\overline {A\cap B} &= \{x\mid x\notin A\cap B\} \\
&   =\{x\mid \lnot(x\in(A\cap B))\} \\
&   =\{x\mid \lnot(x\in A\land x\in B)\} \\
&   =\{x\mid \lnot (x\in A)\lor \lnot(x\in B)\}\\
&   =\{x\mid x\notin A\lor x\notin B\}\\
&   =\{x\mid x\in \overline{A}\lor x\in \overline{B}\} \\
&   =\{x\mid x\in \overline{A}\cup\overline{B}\} \\
&   =\overline{A}\cup\overline{B}
\end{align}
```
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

```math
f(n) =
\begin{cases}
\frac{n}{2},  & \text{if $n$ is even} \\
3n+1, & \text{if $n$ is odd}
\end{cases}
```
$$
f(n) =
\begin{cases}
\frac{n}{2},  & \text{if $n$ is even} \\
3n+1, & \text{if $n$ is odd}
\end{cases}
$$

```math
(x+y)^n=\sum_{j=0}^n\left(\begin{array}{c}n \\r\end{array}\right)x^{n-1}y^i
```
$$(x+y)^n=\sum_{j=0}^n\left(\begin{array}{c}n \\r\end{array}\right)x^{n-1}y^i$$

```math
\left(
    \begin{array}{c}
    n \\
    r
    \end{array}
\right)
```
$$\left(\begin{array}{c}n \\r\end{array}\right)$$

```math
f(x)=\begin{cases}x^2+5\qquad x<0\\
x^3+5x+6\qquad x>0 \end{cases}
```
$$f(x)=\begin{cases}x^2+5\qquad x<0\\
x^3+5x+6\qquad x>0 \end{cases}$$
[更多](http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)
