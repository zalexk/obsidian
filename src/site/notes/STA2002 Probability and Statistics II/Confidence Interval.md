---
{"dg-publish":true,"permalink":"/sta-2002-probability-and-statistics-ii/confidence-interval/","created":"2026-09-22T23:32:14.270+08:00","updated":"2026-09-29T13:52:22.046+08:00","dg-note-properties":{}}
---


> [!important] Definition
> **Confidence Interval**
> Let $X_1, X_2, \cdots, X_{n}$ be a sample on a random variable $X$, where $X$ has PDF $f(x;\theta)$, $\theta\in \Omega$.
> Let $L = L(X_1, \cdots, X_n)$ and $U=U(X_1,\cdots, X_n)$ be 2 statistics.
> Given a level $\alpha \in (0,1)$, if
> $$
> P\{ 
> L(X_1,\cdots, X_n)\le \theta \le U(X_1,\cdots, X_n) 
> \} = 1-\alpha
> $$
> Then, $(L,U)$ is a $(1-\alpha)100\%$ confidence interval for $\theta$.
> The confidence coefficient of the interval is the probability that the interval includes $\theta$ is $1-\alpha$.

> [!note] 一个通俗版本的理解
> If $P\{\hat \theta_{1} \le \theta \le \hat \theta_{2}\} = 1-\alpha$,
> Then, $\left[\hat \theta_1, \hat \theta_2\right]$ is the confidence interval of $\theta$ with confidence coefficient $1-\alpha$.

## Case 1: Normal Distribution （$\sigma^2$ known）
$X_i \sim N(\mu, \sigma^2)$ and $\sigma^2$ is known.
$$
\begin{align}
\bar X &\sim N\left(\mu, \frac{\sigma^2}{n}\right) \\
Z&= \frac{\bar X - \mu}{\frac{\sigma}{\sqrt{n}}}\\ \\
&\sim N(0,1) \\
P\left(-z_{\frac{\alpha}{2}} \le \frac{\bar X - \mu}{\frac{\sigma}{\sqrt{n}}}\le z_{\frac{\alpha}{2}} \right) &= 1-\alpha \\
P\left\{-z_{\frac{\alpha}{2}} \le \frac{\sqrt{n}(\bar X - \mu)}{\sigma}\le z_{\frac{\alpha}{2}} \right\} &= 1-\alpha\\
P\left\{ -\sigma z_{\frac{\alpha}{2}} \le \sqrt{n}(\bar X - \mu) \le \sigma z_{\frac{\alpha}{2}} \right\} &= 1-\alpha \\
P\left\{ - \frac{\sigma z_{\frac{\alpha}{2}}}{\sqrt{ n }} \le \bar X - \mu \le \frac{\sigma z_{\frac{\alpha}{2}}}{\sqrt{n}}  \right\}&= 1-\alpha \\
P\left\{ \bar X + \frac{\sigma z_{\frac{\alpha}{2}}}{\sqrt{n}} \ge \mu \ge \bar X - \frac{\sigma z_{\frac{\alpha}{2}}}{\sqrt{n}}  \right\} &= 1-\alpha \\
P\left\{ \mu \in \left[ \bar{X} \pm \frac{ \sigma z_{\frac{\alpha}{2}}}{\sqrt{n}} \right]  \right\} &= 1-\alpha
\end{align}
$$
$(1-\alpha)$ CI: $[L(X_1, \cdots, X_n), U(X_1,\cdots, X_n)]$ is random
Once the sample is observed,we can compute the sample mean $\bar x$
> [!note]
> **TLDR:**  $\bar x$ 是随机变量 $\bar X$  的一次观测值
> $\bar X$  是随机变量，所以 interval 是随机的；
> 一旦样本观测完，把 $\bar X$ 换成具体数字 $\bar x$，interval 就固定了

The computed interval, $\bar{x} \pm \frac{ \sigma z_{\frac{\alpha}{2}}}{\sqrt{n}}$ is $100(1-\alpha)\%$ , is confidence interval of $\mu$
- CI is centered at $\bar x$ (a point estimate of $\mu$)
- Width: $2z_{\frac{\alpha}{2}}\left( \frac{\sigma}{\sqrt n} \right)$
> [!note]
> 我们使用 $q_{1-\frac{\alpha}{2}}$ 和 $q_{\frac{\alpha}{2}}$ 是为了让置信区间（Confidence Interval）左右对称。
> 这样不仅能最公平地分配误差，而且能让这个区间在数轴上变得最短，从而提高估计的精度。
> $q_{1-\frac{3}{4}\alpha}, q_{\frac{\alpha}{4}}$ 虽然覆盖的面积是对的，但会导致区间“歪”向一边，不够精准。
![CI.png](/img/user/%E9%99%84%E4%BB%B6/CI.png)

| Fixed            | Change              | Width        |
| ---------------- | ------------------- | ------------ |
| $\alpha, \sigma$ | $n\uparrow$         | $\downarrow$ |
| $\sigma, n$      | $\alpha \downarrow$ | $\uparrow$   |
| $\alpha, n$      | $\sigma \uparrow$   | $\uparrow$   |
#### Example
> Let $X$ be the length of lifetime of a light bulb and assume $X\sim N(\mu, 1296)$.
> There are random sample of $n=27$ with $\bar x = 1478$.
> What is the $95\%$ confidence interval?

$$
\begin{align} \\
1-\alpha &= 0.95 \\
\alpha &= 0.05\\
\bar X &\sim N\left( \mu, \frac{1296}{27} \right)  \\
&\sim N\left( \mu, 48 \right) \\
Z &= \frac{\bar X-\mu}{\sqrt{48}} \sim N(0,1) \\

P\left\{ -z_{\frac{0.05}{2}} \le \frac{\bar X-\mu}{\sqrt{48}} \le z_{\frac{0.05}{2}}  \right\}&= 0.95 \\ 
P\{z_{0.025}\sqrt{48}+\bar X \ge \mu \ge \bar X -z_{0.025}\sqrt{48}\} &= 0.95\\
P\left\{\bar X - z_{0.025}\sqrt{48} \le \mu \le \bar X +z_{0.025}\sqrt{48} \right\} &= 0.95 \\
P\{\bar X - 1.96\sqrt{48} \le \mu \le  \bar X + 1.96\sqrt{48}\}&= 0.95 \\
\text{The confidence interval for }\mu &=[\bar x - 13.579, 13.579+\bar x] \\
&= [1478-13.579, 13.579+1478] \\
&= [1464.42, 1491.58]
\end{align}
$$

### Estimation Error
Estimation error $E := |\bar x - \mu|$
> [!note]
> If it is normal distribution and $\sigma^2$ is known, 
> then
> $$
> E\le z_{\frac{\alpha}{2}} \frac{\sigma}{\sqrt{n}}
> $$
### One Sided $\mathbf{(1-\alpha)}$ CI
#### Example 1: Lower bound
$$
\begin{align}
P\{ \theta \ge L(X_{1},\cdots, X_{n})\} &= 1-\alpha \\
P\{h(X_{1},\cdots, X_{n};\theta) \le q_{\alpha} \} &= 1-\alpha \\
h(X_{1},\cdots, X_{n};\theta) &\sim N(0,1)\\
P\left\{ \frac{\sqrt{n} (\bar X - \mu)}{\sigma} \le z_{\alpha}  \right\} &= 1-\alpha \\
P\left\{ \bar X - \mu \le \frac{\sigma z_{\alpha}}{\sqrt{n}} \right\} &= 1-\alpha \\
P\left\{ \mu \ge \bar X - z_{\alpha} \frac{\sigma}{\sqrt{n}}  \right\}&= 1-\alpha
\end{align}
$$
The confidence interval is $\left[\bar x - z_{\alpha} \frac{\sigma}{\sqrt{n}}, +\infty\right)$
#### Example 2: Upper bound

$$
\begin{align}
P\{\theta \le U(X_{1}, \cdots, X_{n})\} &= 1-\alpha \\
P\{h(X_{1},\cdots, X_{n};\theta) \ge q_{1-\alpha}\} &= 1-\alpha \\
h(X_{1},\cdots, X_{n};\theta) &\sim N(0,1) \\
P\left\{ \frac{\sqrt{n}(\bar X - \mu)}{\sigma} \ge -z_{\alpha}  \right\}&= 1-\alpha \\
P\left\{ \bar X - \mu \ge -\frac{\sigma}{\sqrt{n}}z_{\alpha}  \right\} &= 1-\alpha \\
P\left\{ \bar X + z_{\alpha}\frac{\sigma}{\sqrt{n}}\ge \mu \right\} &= 1-\alpha
\end{align}
$$
Hence, confidence interval is $\left( -\infty, \bar X + z_{\alpha} \frac{\sigma}{\sqrt{n}} \right]$
![One-sided CI.png](/img/user/%E9%99%84%E4%BB%B6/One-sided%20CI.png)
## Case 2: Non-Normal Distribution ($\sigma^2$ Known)
$X_1, \cdots, X_n$ are i.i.d. with mean $\mu = \mathbb E(X_1)$ and variance $\sigma^2 = Var(X_1)$, which is known.
By Central Limit Theorem, for large $n$,
$$
\frac{\bar X - \mu}{\frac{\sigma}{\sqrt{n}}}\stackrel{approx}{\sim} N(0,1)
$$
Thus, 
$$
P\left( \bar X - z_{\frac{\alpha}{2}} \frac{\sigma}{\sqrt{n}} \le \mu \le \bar X + z_{\frac{\alpha}{2}} \frac{\sigma}{\sqrt{n}} \right) \approx 1-\alpha
$$
The asymptotic / approximate two-sided $100(1-\alpha)\%$ CI is 
$$
\bar x \pm z_{\frac{\alpha}{2}} \left( \frac{\sigma}{\sqrt{n}} \right)
$$
#### Example
> Let $X$ be amount of orange juice consumed by an American per day
> Given $\sigma = 96, n= 576, \bar x = 133$
> What is the approximate 90% confidence interval for $\mu$

$$
\begin{align}
1-\alpha &= 0.9 \\
\alpha &= 0.1 \\
\text{By CLT, } \frac{\bar X - \mu}{\frac{96}{\sqrt{576}}} &\stackrel{approx}{\sim} N(0,1) \\
\frac{\bar X - \mu}{4} &\stackrel{approx}{\sim} N(0,1) \\
P\left\{ -z_{\frac{\alpha}{2}}  \le \frac{\bar X - \mu}{4} \le z_{\frac{\alpha}{2}} \right\} &= 0.9 \\
P\left\{ 4z_{0.05}+\bar X  \ge \mu \ge \bar X - 4z_{0.05} \right\}&=0.9 \\
P\left\{ \bar X - 4z_{0.05}  \le \mu \le \bar X + 4z_{0.05} \right\}&=0.9  \\
\text{The confidence interval for }\mu  &= [\bar x \pm 4z_{0.05}] \\
&= [133\pm 4\times 1.645] \\
&= [126.42,139.58]
\end{align}
$$
> [!tip]
> Case 1 和 Case 2 做法几乎一样 ——
> Substitute given variables and find the interval
> $$
> \bar x \pm z_{\frac{\alpha}{2}}\left( \frac{\sigma}{\sqrt{n}} \right)
> $$
> 
## Case 3: Normal Distribution ($\sigma^2$ Unknown)
$X_1, \cdots, X_n \sim N(\mu, \sigma^2)$ and $\sigma^2$ is unknown
In [[STA2002 Probability and Statistics II/Confidence Interval#Case 1 Normal Distribution （$ sigma 2$ known）\|#Case 1 Normal Distribution （$ sigma 2$ known）]], $\bar x \pm z_{\frac{\alpha}{2}}\left( \frac{\sigma}{\sqrt{n}} \right)$ depends on $\sigma$.
As $\sigma$ is unknown, we cannot use $\bar x \pm z_{\frac{\alpha}{2}}\left( \frac{\sigma}{\sqrt{n}} \right)$ to find the interval.
Hence, we need to use sample variance $S^2$  and student's theorem
$$
\begin{align}
\text{Sample variance: }S^2 &= \frac{1}{n-1}\sum^n_{i=1}(X_{i} - \bar X)^2 \\
\text{Student's theorem: } \frac{\bar X - \mu}{\frac{S}{\sqrt{n}}} &\sim t(n-1)
\end{align}
$$
Hence, we need to use $\pm t_{\frac{\alpha}{2}}(n-1)$ as upper and lower bound.
$$
\begin{align}
P\left\{ -t_{\frac{\alpha}{2}}(n-1) \le \frac{\bar X - \mu}{\frac{S}{\sqrt{n}}} \le t_{\frac{\alpha}{2}}(n-1)  \right\} &= 1-\alpha \\
P\left\{ - \frac{S \cdot t_{\frac{\alpha}{2}} (n-1)}{\sqrt{n}} \le \bar X - \mu \le \frac{S\cdot t_{\frac{\alpha}{2}}(n-1)}{\sqrt{n}} \right\} &= 1-\alpha \\
P\left\{\bar X- \frac{S\cdot t_{\frac{\alpha}{2}}(n-1)}{\sqrt{n}} \le \mu \le \bar X +  \frac{S\cdot t_{\frac{\alpha}{2}}(n-1)}{\sqrt{n}}  \right\} &= 1-\alpha
\end{align}
$$
The $100(1-\alpha)\%$ CI of $\mu$ is 
$$
\left[ \bar x - \frac{s\cdot t_{\frac{\alpha}{2}}(n-1)}{\sqrt{n}}, \bar x + \frac{s\cdot t_{\frac{\alpha}{2}}(n-1)}{\sqrt{n}} \right]
$$
> [!note]
> $S$ 和 $s$ 的区别跟 $X$ 和 $x$ 的区别一样 ——
> 即 $S$ 是 random variable，而 $s$ 是 observed value

#### Example
> Let $X\sim N(\mu, \sigma^2)$, and both $\mu$ and $\sigma^2$ are unknown
> Given $n=20, \bar x=507.5, s= 89.75, t_{0.05}(19) = 1.729$.
> What is 90% CI for $\mu$?

$$
\begin{align} \\
1-\alpha &= 0.9 \\
\alpha &= 0.1\\
\frac{\bar X - \mu}{\frac{S}{\sqrt{20}}} \sim t(19) \\
P\left\{ -t_{\frac{0.1}{2}} (19) \le  \frac{\bar X - \mu}{\frac{S}{\sqrt{20}}} \le t_{\frac{0.1}{2}}(19) \right\}&= 0.9 \\
P\left\{ - \frac{S \cdot t_{0.05}(19)}{\sqrt{20}} \le \bar X - \mu \le \frac{S \cdot t_{0.05}(19)}{\sqrt{20}}  \right\} &= 0.9 \\
P\left\{\bar X- \frac{S \cdot t_{0.05}(19)}{\sqrt{20}} \le \mu \le \bar X + \frac{S \cdot t_{0.05}(19)}{\sqrt{20}} \right\} &= 0.9 \\
\text{The confidence interval for }\mu &= \left[ \bar x\pm \frac{s\cdot t_{0.05}(19)}{\sqrt{20}}\right] \\
&= \left[ 507.5\pm \frac{89.75\times 1.729}{\sqrt{20}}\right] \\
&= [472.80, 542.20]
\end{align}
$$
## Case 4: Non-Normal Distribution ($\sigma^2$ Unknown)
$X_1, \cdots, X_n$ are i.i.d. with mean $\mu = \mathbb E(X_1)$ and variance $\sigma^2 = Var(X_1)$, which is unknown.
If $n$ is large enough / each $X_i$ is approximately normal, then 
$$
\frac{\bar X - \mu}{\frac{S}{\sqrt{n}}} \stackrel{approx}{\sim} t(n-1)
$$
Approximate two-sided $100(1-\alpha)\%$ CI of $\mu$ is
$$
\left[ \bar x - \frac{s\cdot t_{\frac{\alpha}{2}}(n-1)}{\sqrt{n}}, \bar x + \frac{s\cdot t_{\frac{\alpha}{2}}(n-1)}{\sqrt{n}} \right]
$$
> [!important]
> If $n$ is large enough, then 
> $$
> t_{\frac{\alpha}{2}} (n-1) \approx z_{\frac{\alpha}{2}}
> $$
> Hence, the approximate two-sided $100(1-\alpha)\%$ CI for $\mu$ is
> $$
> \left[ \bar x - z_{\frac{\alpha}{2}}\left( \frac{s}{\sqrt{n}} \right), \bar x + z_{\frac{\alpha}{2}}\left( \frac{s}{\sqrt{n}} \right) \right]
> $$

| Distribution of $X_i$                               | Distribution                                                                  | Two-sided $1-\alpha$ CI                                   |
| :-------------------------------------------------- | :---------------------------------------------------------------------------- | :-------------------------------------------------------- |
| $N(\mu, \sigma^2)$, $\sigma^2$ known                | $\dfrac{\bar{X} - \mu}{\sigma/\sqrt{n}} \sim N(0,1)$                          | $\bar{x} \pm \dfrac{\sigma \cdot z_{\alpha/2}}{\sqrt{n}}$ |
| Any distribution with large $n$, $\sigma^2$ known   | $\dfrac{\bar{X} - \mu}{\sigma/\sqrt{n}} \overset{\text{approx}}{\sim} N(0,1)$ | $\bar{x} \pm \dfrac{\sigma \cdot z_{\alpha/2}}{\sqrt{n}}$ |
| $N(\mu, \sigma^2)$, $\sigma^2$ unknown              | $\dfrac{\bar{X} - \mu}{S/\sqrt{n}} \sim t(n-1)$                               | $\bar{x} \pm \dfrac{s \cdot t_{\alpha/2}(n-1)}{\sqrt{n}}$ |
| Any distribution with large $n$, $\sigma^2$ unknown | $\dfrac{\bar{X} - \mu}{S/\sqrt{n}} \overset{\text{approx}}{\sim} t(n-1)$      | $\bar{x} \pm \dfrac{s \cdot t_{\alpha/2}(n-1)}{\sqrt{n}}$ |
