---
{"dg-publish":true,"permalink":"/sta-2002-probability-and-statistics-ii/order-statistic/","created":"2026-11-21T18:38:12.201+08:00","updated":"2026-11-22T00:47:12.318+08:00","dg-note-properties":{}}
---


> [!important] Definition
> Suppose that $X_1, \cdots, X_n$ are i.i.d. random samples from a common distribution.
> For any $k=1,2,\cdots, n$, the $k$-th order statistic is the random variable
> $$ X_{(k)} = k \text{-th smallest of } X_{1}, \cdots, X_{n}$$

> [!note]
> The order statistics for $\begin{cases}X_1&=1\\ X_2&=3\\ X_3&=2\\ X_4&=2 \end{cases}$ are $\begin{cases}X_{(1)}&=1\\ X_{(2)}&=2\\ X_{(3)}&=2\\ X_{(4)}&=3\end{cases}$

#### Example
> Let $X_1, \cdots, X_5$ be i.i.d. random samples from the PDF
> $$ f(x) = 2x, \quad 0< x<1$$
> Its CDF is 
> $$ F(x) = \int^x_{0} 2y\ dy = x^2,\quad 0<x<1$$
> The observed values are 
> $$\begin{cases}x_{1} &= 0.62\\ x_{2} &= 0.98\\ x_{3} &= 0.31\\ x_{4} &= 0.81\\ x_{5} &= 0.53\end{cases}$$

The observed order statistics are
$$
\begin{cases}
x_{(1)} &= 0.31 \\
x_{(2)} &= 0.53 \\
x_{(3)} &= 0.62 \\
x_{(4)} &= 0.81  \\
x_{(5)} &= 0.98
\end{cases}
$$
The CDF of $X_{(5)}$ is 
$$
\begin{aligned}
\Pr(X_{(5)} \le x) &= \Pr( \max\{ X_{1}, X_{2}, X_{3}, X_{4} ,X_{5}\} \le x) \\
&= \Pr(X_{1} \le x, X_{2} \le x, X_{3} \le x, X_{4} \le x, X_{5} \le x) \\
&= \prod^5_{i=1} \Pr(X_{i} \le x) \\
&= F(x)^5 \\
&= (x^{2})^5 \\
&= x^{10} \\
f_{X_{(5)}} (x) &= \frac{d}{dx}x^{10} \\
&= 10x^9 \\
&= 5F(x)^4 f(x)
\end{aligned}
$$
The CDF of $X_{(4)}$ is 
$$
\begin{aligned}
\text{Let }W &= \text{number of $X_i$ s.t. }X_{i} \le x \\
W&\sim \text{Bin}(5, F(x)) \\
\Pr(X_{(4)} \le x) &= \Pr(W \ge 4) \\
&= \Pr(W = 4) + \Pr(W=5) \\
&= \binom{5}{4} F(x)^4 [1-F(x)] + F(x)^5
\end{aligned}
$$
The PDF of $X_{(4)}$ is 
$$
\begin{aligned}
f_{X_{(4)}} (x) &= \frac{d}{dx} F_{X_{(4)}}(x)  \\
&= \frac{d}{dx} \left\{\binom{5}{4} F(x)^4 [1-F(x)] + F(x)^5\right\} \\
&= \frac{d}{dx} \left\{\binom{5}{4} F(x)^4  - \binom{5}{4}F(x)^5 + F(x)^5\right\} \\
&= \binom{5}{4} 4 F(x)^3 f(x)  - \binom{5}{4}5F(x)^4 f(x) + 5F(x)^4 f(x) \\
&= \binom{5}{4} F(x)^3 f(x) [4-5F(x)]+5F(x)^4 f(x)\\
&= 5F(x)^3 f(x) [4-5F(x)]+5F(x)^4 f(x) \\
&= 5F(x)^3 f(x) [4-5F(x) + F(x)] \\
&= 20F(x)^3f(x)[1-F(x)]
\end{aligned}
$$
> [!tip]
> $W$ 是 $X_i \le x$ 的数量
> 因此，计算 $\Pr(W \ge 4)$ 即是计算 「有 4  个或以上的 $X_i \le x$ 的概率」


> [!important]
> Suppose $X_1 , \cdots, X_{n}$ are i.i.d. continuous random variable with common PDF $f(x)$ and CDF $F(x)$.
> For $k=1,\cdots, n$, denote the CDF and PDF of the $k$-th order statistic $X_{(k)}$ to be $F_{X_{(k)}}$ and $f_{X_{(k)}}$ respectively.
> $$
> \begin{aligned}
> F_{X_{(k)}}(x) &= \sum^n_{l=k} \binom{n}{l} F(x)^l [1-F(x)]^{n-l} \\
> f_{X_{(k)}}(x) &= \frac{n!}{(k-1)!1! (n-k)!} [F(x)]^{k-1} f(x) [1-F(x)]^{n-k}
> \end{aligned}
> $$

| 因子                               | 取值范围     | 含义                                                                   |
| -------------------------------- | -------- | -------------------------------------------------------------------- |
| $\dfrac{n!}{(k-1)!\,1!\,(n-k)!}$ | 正整数      | 多项系数：把 $n$ 个观测分成 “左边 $k-1$ 个 / 正好在 $x$ 处 1 个 / 右边 $n-k$ 个” 三组，有多少种分法 |
| $[F(x)]^{k-1}$                   | $0\sim1$ | 那 $k-1$ 个都落在 $x$ 左边的概率                                               |
| $f(x)$                           | $\ge0$   | 恰有 1 个落在 $x$ 附近（密度，不是概率）                                             |
| $[1-F(x)]^{n-k}$                 | $0\sim1$ | 剩下 $n-k$ 个都落在 $x$ 右边的概率                                              |

![General Form of Order Statistics.png](/img/user/STA2002%20Probability%20and%20Statistics%20II/Attachment/General%20Form%20of%20Order%20Statistics.png)
## Order Statistics of Uniform Distribution
Suppose $U_1, \cdots, U_n \overset{\text{i.i.d.}}{\sim} \text{Uniform}(0,1)$
$$
\begin{aligned}
F_{U_{1}} (x) &= x, \quad 0< x< 1 \\
f_{U_{1}} (x) &= 1
\end{aligned}
$$
Denote the order statistics by $U_{(1)}, \cdots, U_{(n)}$
The PDF of $U_{(k)}$ for $k=1,\cdots, n$ is 
$$
\begin{aligned}
f_{U_{(k)}} (x) &= \frac{n!}{(k-1)! 1! (n-k)!} x^{k-1} (1-x)^{n-k} \\
&= \frac{(k-k+n-1+1)!}{(k-1)!(n-k+1-1)!} x^{k-1} (1-x)^{n-k+1-1} \\
&= \frac{\Gamma(k+n-k+1)}{\Gamma(k) \Gamma(n-k+1)} x^{k-1} (1-x)^{n-k+1-1}
\end{aligned}
$$
> [!note]
> $$\Gamma(k) = (k-1)! = \int^\infty_{0} x^{k-1}e^{-x}$$

> [!important] Beta Distribution
> For $X\sim \text{Beta}(\alpha, \beta)$, its PDF is 
> $$f(x) = \frac{\Gamma(\alpha + \beta)}{\Gamma(\alpha)\Gamma(\beta)} x^{\alpha - 1} (1-x)^{\beta - 1}, \quad 0<x<1$$
> - $\mathbb E(x) = \dfrac{\alpha}{\alpha + \beta}$
> - $Var(X) = \dfrac{\alpha\beta}{(\alpha + \beta +1)(\alpha + \beta)^2}$

For uniform distribution,
$$
U_{(k)} \sim \text{Beta}(k, n-k+1)
$$
- $\mathbb E[U_{(k)}] = \dfrac{k}{n+1}$
- $Var[U_{(k)}] = \dfrac{k(n-k+1)}{(n+1)^2 (n+2)}$

## Distributions of $F(X_{(k)})$
Suppose $X_1, \cdots, X_n$ are i.i.d. continuous random variables with strictly increasing CDF $F$
Define $Y=F(X_k)$, then its CDF is 
$$
\begin{aligned}
\Pr(Y\le y) &= \Pr\{F(X_{k})\le y\} \\
&= \Pr\{X_{k} \le F^{-1}(y) \} \\
&= F\{F^{-1}(y) \} \\
&= y
\end{aligned}
$$
$\Pr(Y\le y) = y$ is CDF of $\text{Uniform}(0,1)$
> [!important]
> $$F(X_k) \sim \text{Uniform}(0,1)$$


Since CDF $F$ is strictly increasing,
$$
X_{i} < X_{j} \iff F(X_{i}) < F(X_{j})
$$
Thus, $F(X_{(k)})$ is the $k$-th smallest of $F(X_1), \cdots, F(X_n)$
Let $U_i = F(X_i)$ be a sequence of i.i.d. $\text{Uniform}(0,1)$ random variables.
Hence, $F(X_(k))$ has the same distribution as $U_{(k)}$
> [!important]
> $$F(X_{(k)}) \sim \text{Beta}(k, n-k+1)$$



