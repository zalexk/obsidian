---
{"dg-publish":true,"permalink":"/csc-3001-discrete-math/mid-terms-revision/","created":"2026-11-08T00:37:43.156+08:00","updated":"2026-11-08T02:38:18.519+08:00","dg-note-properties":{}}
---


## Recursion

| Sequence                 | Example                                                      | Recursive definition                                                  | Sum                                                            |
| ------------------------ | ------------------------------------------------------------ | --------------------------------------------------------------------- | -------------------------------------------------------------- |
| Arithmetic sequence 等差数列 | $\{a, a+d, a+2d, a+3d, \cdots\}$                             | $\begin{cases}a_0&=a\\ a_{i+1}&= a_i+d\end{cases}$                    | $\dfrac{[2 a+(n-1)d]n}{2}$                                     |
| Geometric sequence 等比数列  | $\{a, ra, r^2 a, r^3 a\}$                                    | $\begin{cases}a_{0}&= a \\  a_{i+1}&=ra_{i}\end{cases}$               | $\dfrac{a(r^n-1)}{r-1} / \dfrac{a(1-r^n)}{1-r}/\dfrac{a}{1-r}$ |
| Harmonic sequence 调和数列   | $\left\{ 1,  \frac{1}{2}, \frac{1}{3}, \frac{1}{4} \right\}$ | $\begin{cases}a_{0}&=1 \\  a_{i+1}&=\dfrac{(i+1)a_i}{i+2}\end{cases}$ |                                                                |
#### Example
> Let $a_0 = 0$ and $a_n = 2 a_{n-1} + n$ ($n\ge 1$)
> Find the closed form for $a_n$.

$$
\begin{aligned}
\text{Try unrolling:}  \\
a_{n} &= 2 a_{n-1} + n \\
&= 2[2a_{n-2} + (n-1)]+n \\
&= 4a_{n-2} + 2(n-1) + n \\
&= 4(2a_{n-3} + (n-2))+ 2(n-1) + n \\
&= 8a_{n-3} + 4(n-2) + 2(n-1) + n \\
&= 2^k a_{n-k} + \sum^{k-1}_{j=0}2^j(n-j), \quad 0\le k \le n \\
&= 2^n a_{0} + \sum^{n-1}_{j=0} 2^j(n-j) \\
&= \sum^{n-1}_{j=0} 2^j(n-j) \\
\text{Let } i &= n-j \\
j &= n-i \\
\text{When } j&= n-1,  \\
i &= 1 \\
a_{n} &= \sum^n_{i=1} 2^{n-i} \cdot i \\
&= 2^n \sum^n_{i=1} \frac{i}{2^i} \\
\text{Let }S&= \sum^n_{i=1} \frac{i}{2^i} \\
&= \frac{1}{2} + \frac{2}{4}+\frac{3}{8} + \frac{4}{16} + \cdots + \frac{n}{2^n} \\
\frac{1}{2} S &= \sum^n_{i=1} \frac{i}{2^{i+1}} \\
&= \frac{1}{4}+\frac{2}{8}+ \frac{3}{16} + \frac{4}{32} + \cdots + \frac{n-1}{2^n} + \frac{n}{2^{n+1}} \\
S-\frac{1}{2}S &= \underbrace{\frac{1}{2} + \frac{1}{4} + \frac{1}{8} + \frac{1}{16} + \cdots + \frac{1}{2^n}}_{1-\frac{1}{2^n}} - \frac{n}{2^{n+1}},\quad \text{错位相减法} \\
\frac{1}{2}S  &= \left( 1-\frac{1}{2^n} \right) - \frac{n}{2^{n+1}} \\
S &= 2\left( 1-\frac{1}{2^n}  - \frac{n}{2^{n+1}} \right) \\
&= 2-\frac{2}{2^n} -\frac{n}{2^{n}} \\
&= 2-\frac{2+n}{2^n} \\
a_{n} &= 2^n S \\
&= 2^{n+1}  - 2-n
\end{aligned}
$$
### Telescoping Sum
$$
\sum_{k=1}^{n}\Big[f(k)-f(k-1)\Big]=f(n)-f(0)
$$
#### Example
> Find $\sum^n_{k=1} \frac{1}{k(k+1)}$

$$
\begin{aligned}
\frac{1}{k(k+1)} &= \frac{A}{k} + \frac{B}{k+1} \\
&= \frac{A(k+1)+Bk}{k(k+1)} \\
&= \frac{(A+B)k + A}{k(k+1)} \\
\text{Comparing the coeff. of like terms, } \ 
&\begin{cases}
A&= 1 \\
B&= -1
\end{cases} \\
\sum^n_{k=1} \frac{1}{k(k+1)} &= \sum^n_{k=1} \left( \frac{1}{k} - \frac{1}{k+1} \right) \\
\text{Let } f(k)&= -\frac{1}{k+1} \\
\sum^n_{i=0} [f(k) - f(k-1)] &= \sum^n_{i=0} \left[ -\frac{1}{k+1} +\frac{1}{k-1+1} \right] \\
&= \sum^n_{i=0} \left[ -\frac{1}{k+1} + \frac{1}{k} \right] \\
&= f(n) - f(0) \\
&= -\frac{1}{n+1} +1 \\
&= \frac{-1 + n+1}{n+1} \\
&= \frac{n}{n+1}
\end{aligned}
$$
> Find  $S= \sum^n_{i=1} \frac{i}{2^i}$

$$
\begin{aligned}
f(i) - f(i-1) &= \frac{Ai+B}{2^i} - \frac{A(i-1)+B}{2^{i-1}} \\
&= \frac{Ai+B}{2^i} - \frac{2[A(i-1)+B]}{2^i} \\
&= \frac{Ai + B-2A(i-1) - 2B}{2^i} \\
&= \frac{Ai-2Ai+2A-B}{2^i} \\
\frac{i}{2^i}&= \frac{-Ai + (2A-B)}{2^i} \\
\text{Comparing the coeff. of like terms, }  &
\begin{cases}
A&= -1 \\
B&=-2
\end{cases} \\
f(i) &= \frac{-i-2}{2^i} \\
&= -\frac{i+2}{2^i} \\
\sum^n_{k=1} [ f(i) - f(i-1)]&= f(n) - f(0) \\
&= -\frac{n+2}{2^n} +2 \\
&= 2-\frac{n+2}{2^n} \\
&= \frac{2^{n+1}-n+2}{2^n}
\end{aligned}
$$
## Generating Functions
> [!important] Ordinary Generating Function (OGF)
> Given a sequence $\{a_n \}_{n\ge 0}$, its OGF is 
> $$
> A(x) = \sum^\infty_{n=0}a_{n} x^n
> $$

> [!important] Basic Operations on OGFs
> - Scaling: $C(x) = \sum \lambda a_n x^n = \lambda A(x)$
> - Addition: $C(x) = A(x) + B(x)$
> - Right shifting (index shift): $C(x) = \sum_{n\ge k}a_{n-1}x^n = x^k A(x) = x^k \sum_{n\ge 0} a_{n} x^n$
> - Differentiation: $A'(k) = \sum_{n\ge 1} na_n x^{n-1}$

![Pasted image 20261108020454.png](/img/user/Pasted%20image%2020261108020454.png)
![Pasted image 20261108020501.png](/img/user/Pasted%20image%2020261108020501.png)
#### Example
> Find the ordinary generating function for the sequence $a_n = n$ for $n\ge 0$.
> $$A(x) = \sum^\infty_{n=0} nx^n$$

$$
\begin{aligned}
\text{Start from GS, } 
A(x) &= \sum^\infty_{n=0} x^n  \\
&= 1+x + x^2 + \cdots \\
\sum^\infty_{n=0} x^n &= \frac{1}{1-x} \\
\sum^\infty_{n=0} nx^{n-1} &= \frac{1}{(1-x)^2}\\
\sum^\infty_{n=0} nx^n &= \frac{x}{(1-x)^2}
\end{aligned}
$$
## Distinct-Roots Theorem
只要递推式是 $a_n=Aa_{n-1}+Ba_{n-2}$, 它的特征方程 是 $t^2-At-B=0$
如果特征方程有两个不同的根 $r,s$，那么通解是 $a_n=Cr^n+Ds^n$
#### Example
> $a_n = a_{n-1} + 2 a_{n-2}$

The characteristic equation is $t^2 - t-2=0$
$$
\begin{aligned}
t^2 - t - 2 &= 0 \\
(t-2)(t+1) &= 0 \\
t &= 2 \quad or \quad -1 \\
a_{n} &= C_{2}^n +D(-1)^n
\end{aligned}
$$
## Cauchy Product
$$
\begin{aligned}
P(x) &= \sum_{i\ge 0} p_i x^i \\
Q(x) &= \sum_{j\ge 0} q_j x^j \\
(p_{x}x^i)(q_{j}x^j) &= p_{i} q_{j}x^{i+j} \\
P(x) Q(x) &= \boxed{\sum_{n\ge 0} \left( \sum^n_{i=0} p_{i}q_{n-i} \right) x^n}
\end{aligned}
$$
#### Example
> The Catalan numbers $(C_n)_{n\ge 0}$ satisfy $$C_0=1, \quad C_{n+1} = \sum^n_{i=0} C_i C_{n-i}\quad (n\ge 0)$$
> Let $C(x) = \sum_{n\ge 0}C_n x^n$ be the OGF. 
> Show that $$C(x) = 1+xC(x)^2$$
> and find a closed express for the power series $C(x)$.

1. Show that $C(x) = 1+xC(x)^2$
$$
\begin{aligned}
C_{n+1} &= \sum^n_{i=0} C_i C_{n-i} \\
C_{n+1}x^{n+1} &= \sum^n_{i=0} C_i C_{n-i} x^{n+1} \\
\sum_{n\ge 0} C_{n+1}x^{n+1} &= \sum_{n\ge 0} \left( \sum^n_{i=0} C_{i} C_{n-i} \right) x^{n+1} \\
C_{1}x + C_{2}x^2 + C_{3}x^3 + \cdots &= \sum_{n\ge 0} \left( \sum^n_{i=0} C_{i} C_{n-i} \right) x^{n+1} \\
C(x) &= C_{0} + C_{1}x + C_{2}x^2 + \cdots \\
&= C_{0} + \sum_{n\ge 0} C_{n+1}x^{n+1} \\
&= 1 + \sum_{n\ge 0} C_{n+1}x^{n+1} \\
\sum_{n\ge 0} C_{n+1}x^{n+1} &= \sum_{n\ge 0} \left( \sum^n_{i=0} C_{i} C_{n-i} \right) x^{n+1} \\
1-C(x) &= \sum_{n\ge 0} \left( \sum^n_{i=0} C_{i} C_{n-i} \right) x^{n+1} \\
&= xC(x)C(x) \\
&= xC(x)^2 \\
C(x)&=1-xC(x)^2
\end{aligned}
$$
2. Find closed form
$$
\begin{aligned} 
\text{Denote }C(x) &= C \\
C &= 1-xC^2 \\
xC^2 - C + 1 &= 0 \\
C &= \frac{1\pm \sqrt{1-4x}}{2x} \\
C_{+}(x) &= \frac{1+\sqrt{1-4x}}{2x} \to \infty  \\
C_{-}(x) &= \frac{1-\sqrt{1-4x}}{2x} \\
&=  \frac{1-\sqrt{1-4x}}{2x} \left( \frac{1+\sqrt{1-4x}}{1+\sqrt{1-4x}} \right) \\
&= \frac{1-(1-4x)}{2x(1+\sqrt{1+4x})} \\
&= \frac{2}{1+\sqrt{1+4x}} \\
C_{-}(0)&= 1 \\
C(x) &= \frac{1-\sqrt{1-4x}}{2x} 
\end{aligned}
$$
---
## Appendix
### 广义二项式定理 Generalized Binomial Theorem

|      | 经典版（classical）                          | 广义版（generalized）                                                  |
| ---- | --------------------------------------- | ----------------------------------------------------------------- |
| 公式   | $(1+y)^m=\sum_{n=0}^{m}\binom{m}{n}y^n$ | $(1+y)^{\alpha}=\sum_{n=0}^{\infty}\binom{\alpha}{n}y^n$          |
| 上标要求 | $m$ 必须是**非负整数**                         | $\alpha$ 可以是**任意实数**（$1/2,\,-1,\,-2/3$…）                          |
| 项数   | 有限，共 $m+1$ 项（terminating）               | 无穷多项（infinite series）                                             |
| 系数   | $\binom{m}{n}=\frac{m!}{n!(m-n)!}$      | $\binom{\alpha}{n}=\frac{\alpha(\alpha-1)\cdots(\alpha-n+1)}{n!}$ |
| 成立范围 | 恒等式，对任意 $y$                             | 只在 $\lvert y\rvert<1$ 收敛                                          |

**广义二项式系数（Generalized binomial coefficient）：** $\binom{\alpha}{n}=\frac{\alpha(\alpha-1)(\alpha-2)\cdots(\alpha-n+1)}{n!}$
> [!note]
> $\binom{\alpha}{n}$ 就是 $f(y)=(1+y)^\alpha$ 在 $y=0$ 处的第 $n$ 阶泰勒系数 $\frac{f^{(n)}(0)}{n!}$，算一下就得到连乘式。
> $$
> \dfrac{f^{(n)}(0)}{n!}=\dfrac{\alpha(\alpha-1)\cdots(\alpha-n+1)}{n!}=\binom{\alpha}{n}
> $$
> 所以「广义二项式定理」本质就是把函数在 $0$ 处做泰勒展开（Taylor expansion）。

