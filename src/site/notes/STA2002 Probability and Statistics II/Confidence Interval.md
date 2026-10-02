---
{"dg-publish":true,"permalink":"/sta-2002-probability-and-statistics-ii/confidence-interval/","created":"2026-09-22T23:32:14.270+08:00","updated":"2026-10-03T00:35:33.947+08:00","dg-note-properties":{}}
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

## CI for Mean $\mu$
### Case 1: Normal Distribution （$\sigma^2$ known）
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

#### Estimation Error
Estimation error $E := |\bar x - \mu|$
> [!note]
> If it is normal distribution and $\sigma^2$ is known, 
> then
> $$
> E\le z_{\frac{\alpha}{2}} \frac{\sigma}{\sqrt{n}}
> $$
#### One Sided $\mathbf{(1-\alpha)}$ CI
##### Example 1: Lower bound
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
##### Example 2: Upper bound

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
### Case 2: Non-Normal Distribution ($\sigma^2$ Known)
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
### Case 3: Normal Distribution ($\sigma^2$ Unknown)
$X_1, \cdots, X_n \sim N(\mu, \sigma^2)$ and $\sigma^2$ is unknown
In [[STA2002 Probability and Statistics II/Confidence Interval#Case 1 Normal Distribution （$ sigma 2$ known）\|#Case 1 Normal Distribution （$ sigma 2$ known）]], $\bar x \pm z_{\frac{\alpha}{2}}\left( \frac{\sigma}{\sqrt{n}} \right)$ depends on $\sigma$.
As $\sigma$ is unknown, we cannot use $\bar x \pm z_{\frac{\alpha}{2}}\left( \frac{\sigma}{\sqrt{n}} \right)$ to find the interval.
Hence, we need to use sample variance $S^2$  and Student's theorem
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
### Case 4: Non-Normal Distribution ($\sigma^2$ Unknown)
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
## CI for the Difference of 2 Means
For
$$
\begin{align}
X_{1}, \cdots, X_{n} &\sim N(\mu_{X},\sigma^2_{X}) \\
Y_{1}, \cdots, Y_{m} &\sim N(\mu_{Y}, \sigma^2_{Y})
\end{align}
$$
To construct confidence intervals for $\mu_X - \mu_Y$, we need to consider 3 cases
- Pooled $t$-interval
	- $X_{1}, \cdots, X_{n}, Y_{1}, \cdots, Y_{m}$ are independent
	- $\sigma^2_X =\sigma^2_Y = \sigma^2$
	- $\sigma^2$ is unknown
- Welch's $t$-interval
	- $X_{1}, \cdots, X_{n}, Y_{1}, \cdots, Y_{m}$ are independent
	- $\sigma^2_{X} \ne \sigma^2_{Y}$ are both unknown
- Paired $t$-interval
	- $X_i, Y_{i}$ are dependent for each $i$
	- Pairs $(X_i, Y_i)$ are independent
	- $\sigma^2_X, \sigma_Y^2$ are unknown
### Case 1: Pooled $t$-interval
Let $X_1, \cdots, X_n \sim N(\mu_{X}, \sigma^2)$ and $Y_1,\cdots, Y_m \sim N(\mu_Y, \sigma^2)$ be independent random variables.
Then, $100(1-\alpha)\%$ CI for $\mu_X-  \mu_Y$ is 
$$
\bar X - \bar Y \pm t_{\frac{\alpha}{2}}(n+m-2)S_{p}\sqrt{\frac{1}{n} + \frac{1}{m}}
$$
$S_p^2$ is pooled estimator of $\sigma^2$, which is unbiased estimator of $\sigma^2$
$$
S^2_{p} = \frac{(n-1)S^2_{X} + (m-1)S^2_{Y}}{n+m-2} = \frac{\sum_{i=1}^n (X_{i} - \bar X)^2 + \sum^m_{i=1}(Y_{i} - \bar Y)^2}{n+m-2}
$$
#### Example
> Let $X \sim N(\mu x, \sigma^2)$ be the score on a standardized test in a large high school.
> Let $Y\sim N(\mu_Y, \sigma^2)$ be the score on a standardized test in a small high school.
> Given: 
> $n=9,\quad \bar x = 81.31,\quad s^2_{x} = 60.76$
> $m=15, \quad \bar y = 78.61,\quad   s_y^2 = 48.24$
> What is 95% confidence interval for $\mu_x - \mu_y$
{ #fd6a48}


$$
\begin{align} 
1-\alpha &= 0.95 \\ 
\alpha &= 0.05\\
n+m-2 &= 22 \\
t_{\frac{1-0.95}{2}}(22) &= 2.074 \\
t_{0.025}(22) &= 2.074 \\
s_{p}^2 &= \frac{8(60.76) + 14(48.24)}{22} \\
s_{p} &= \sqrt{\frac{486.08 + 675.36}{22}} \\
\text{Confidence interval for } \mu_{X} - \mu_{Y} &= 81.31- 78.61 \pm 2.074 \left( \sqrt{\frac{486.08 + 675.36}{22}} \right)\left( \sqrt{\frac{1}{9}+ \frac{1}{15}} \right) \\
&= [-3.65, 9.05]
\end{align}
$$
### Case 2: Welch's $t$-interval
Let $X_1, \cdots, X_n \sim N(\mu_{X}, \sigma^2_{X}), \quad Y_{1}, \cdots, Y_{m} \sim N(\mu_{Y}, \sigma^2_{Y})$ be independent
Approximate $100(1-\alpha)\%$ CI for $\mu_X - \mu_Y$ is 
$$
\bar X - \bar Y \pm t_{\frac{\alpha}{2}}(r) \sqrt{\frac{S^2_{X}}{n} + \frac{S^2_{Y}}{m}}
$$
where 
$$
r=\left\lfloor\frac{\left(\dfrac{S_X^2}{n}+\dfrac{S_Y^2}{m}\right)^2}{\dfrac{1}{n-1}\left(\dfrac{S_X^2}{n}\right)^2+\dfrac{1}{m-1}\left(\dfrac{S_Y^2}{m}\right)^2}\right\rfloor
$$

> [!note]
> $\lfloor x \rfloor$ is floor function (round down)
> i.e.  $\lfloor 3.4\rfloor = \lfloor 3.9 \rfloor = 3$

> [!note]
> - Welch 公式算出来的自由度 $r$ 通常不是整数（比如 19.8），但 t 分布表只有整数自由度，必须取一个整数去查表
> - 而「向下取整」比「向上取整/四舍五入」更保守、更安全--它让区间更宽，绝不会把真实置信水平说低
#### Example
> Assume $\sigma^2_X \ne \sigma^2_Y$
> Scenario is same as [[STA2002 Probability and Statistics II/Confidence Interval#^fd6a48\|#^fd6a48]]

$$
\begin{align}
\alpha &= 0.05 \\
r &= \left \lfloor  
\frac{\left( \frac{60.76}{9} + \frac{48.24}{15} \right)^2}{\frac{1}{8} \left( \frac{60.76}{9} \right)^2 + \frac{1}{14}\left( \frac{48.24}{15} \right)^2}
\right  \rfloor  \\
&= 15 \\
t_{0.025}(15)&= 2.131 \\
\text{Welch's $t$-interval for }\mu_{X} - \mu_{Y} &= 81.31-78.61 \pm 2.131\left( \sqrt{\frac{60.76}{9} + \frac{48.24}{15}} \right) \\
&= [-4.0278, 9.4278]
\end{align}
$$

Compared to pooled $t$-interval $[-3.65, 9.05]$, Welch's $t$-interval is wider than pooled $t$-interval.  
### Case 3: Paired $t$-interval
> [!important] Definition
> **Paired samples**
> Each data point in the first sample is matched & related to a unique data point in the second sample
> ![paired_sample.png](/img/user/%E9%99%84%E4%BB%B6/paired_sample.png)

Let $(X_1, Y_1), \cdots, (X_n, Y_n)$ be $n$ pairs of dependent measures.
Let $D_i = X_i-Y_i$. 
Suppose $D_1, \cdots, D_n \sim N(\mu_{D}, \sigma^2_{D})$ with $\mu_D = \mu_X - \mu_Y$.
Then, $100(1-\alpha)\%$ CI for $\mu_X - \mu_Y$ is
$$
\bar D \pm t_{\frac{\alpha}{2}} (n-1) \frac{S_{D}}{\sqrt{n}}
$$
where 
$$
\begin{align}
\bar D &= \frac{1}{n}\sum^n_{i=1}D_{i} \\
S^2_{D} &= \frac{1}{n-1} \sum^n_{i=1}(D_{i} - \bar D)^2
\end{align}
$$
> [!note]
> **配对的目的是“消掉个体之间的差异”**
> 以减肥药为例 —— 有人天生体重就高（比如 90 kg），有人天生低（比如 50 kg）。
> 如果我用"服药后组 vs 服药前组"来比，即使药完全无效，两组的个体构成稍有不同（比如高体重的人恰好多分了几个到"服药后"组），均值就会差出好几公斤。
> **这个"个体差异"造成的噪声，把真正的药效完全盖住了。**
>
> 配对的做法是**同一个人自己和自己比**：$D_i = \text{服药后}_i-\text{服药前}_i$。
> 这个差值里，"这个人天生体重多少"**被减掉了** —— 它同时出现在 $X_i$ 和 $Y_i$ 里，一减就没了。
> 剩下的 $D_i$ 只包含"药效 + 这一次测量的随机误差"。

#### Example
> An experiment was conducted to compare people's reaction times to a red light versus green light.
> When signaled with either red or green light, the subject was asked to hit a switch to turn off the light
> When the switch was hit, a clock was turned off and the reaction time was recorded
>
> Given $n = 8, \bar d = -0.062, s_{d} = 0.0765$
> What is the 95% CI for $\mu_X - \mu_Y$?

| Subject | Red ($x$) | Green ($y$) | $d = x - y$ |
|:-------|:---------|:-----------|:-----------|
| 1       | 0.30      | 0.43        | −0.13       |
| 2       | 0.23      | 0.32        | −0.09       |
| 3       | 0.41      | 0.58        | −0.17       |
| 4       | 0.53      | 0.46        | 0.07        |
| 5       | 0.24      | 0.27        | −0.03       |
| 6       | 0.36      | 0.41        | −0.05       |
| 7       | 0.38      | 0.38        | 0.00        |
| 8       | 0.51      | 0.61        | −0.10       |

$$
\begin{align}
-0.0625 \pm t_{0.025}(7) \left( \frac{0.0765}{\sqrt{8}} \right) = [-0.1265, 0.0015]
\end{align}
$$
Using pooled and Welch's $t$-interval to calculate CI,
Given that $\bar x = 0.3700, \bar y = 0.4325, s_X = 0.1124, s_Y = 0.1173$.
**Pooled $t$-interval**
$$
\begin{align}
95\% CI &= 0.3700 - 0.4325 \pm t_{0.025}(14) \sqrt{\frac{7(0.1124)^2 + 7(0.1173)^2}{14}} \sqrt{\frac{2}{8}} \\
&= [-0.1857, 0.0607]
\end{align}
$$
**Welch's $t$-interval**
$$
\begin{align} \\
r &= \left \lfloor \frac{\left( \frac{0.1124^2}{8} + \frac{0.1173^2}{8} \right)^2}{\frac{1}{7}\left( \frac{0.1124^2}{8} \right)^2 + \frac{1}{7} \left( \frac{0.1173^2}{8} \right)^2}
\right \rfloor \\
&= 13\\
95\% CI &= 0.3700-0.4325 \pm t_{0.025} (13) \sqrt{\frac{0.1124^2}{8} + \frac{0.1173^2}{8}} \\
&= [-0.1865, 0.0615]
\end{align}
$$
With same center $\bar d = \bar x- \bar y$, CI widths are different
**In general, CI width:** Pair $t$-interval < Pool $t$-interval < Welch's $t$-interval

> [!note]
> When $s^2_X$ is closed to $s^2_Y$, widths of pooled $t$-interval and Welch's $t$-interval are similar.

## CI for Proportions
#### Example
> In a political campaign survey, we collect a sample of $n=351$ voters.
> $y=185$ out of them favor candidate A and remaining favour candidate B.
> Let $p$ be the supporting rate in the population. 
> How to build a CI for the supporting rate?

$$
\begin{align}
\text{Let }X_i &=  
\begin{cases}  & 
 1, \quad &\text{favour candidate A}  \\ 
0, &\text{favour candidate B} 
\end{cases} \\
X_{1},\cdots, X_{n} &\sim \text{Bernoulli}(p) \\
\text{Denote } Y&= \sum_{i=1}^n X_{i} \sim \text{Bin}(n,p)\\
\text{By CLT }, 
\frac{Y-np}{\sqrt{np(1-p)}} &\overset{\text{approx}}{\sim} N(0,1)  \\  \\

\text{By MLE,} \\
L(p) &= \prod^n_{i=1}p^{X_{i}}(1-p)^{1-X_{i}} \\
&= p^{\sum_{i=1}^n X_{i}}(1-p)^{n-\sum_{i=1}^n X_{i}} \\
&= p^Y (1-p)^{n-Y} \\
\ell(p)&= Y\ln p + (n-Y)\ln(1-p) \\
\ell'(p) &= 0 \\
\frac{Y}{p} - \frac{n-Y}{1-p} &= 0 \\
\frac{Y}{p} &= \frac{Y-n}{p-1} \\
Y(p-1)&= p(Y-n) \\
Yp - Y &= pY - pn \\
\hat p &= \frac{Y}{n} \\ 
&= \frac{185}{351} \\
&\approx 0.527 \\
 \\

Y&= n\hat p \\
P\left\{ -z_{\frac{\alpha}{2}} \le \frac{Y-np}{\sqrt{np(1-p)}}  \le z_{\frac{\alpha}{2}} \right\} &\approx 1-\alpha \\
P\left\{ -z_{\frac{\alpha}{2}} \le \frac{n(\hat p - p)}{\sqrt{n}\sqrt{p(1-p)}}  \le z_{\frac{\alpha}{2}} \right\} &\approx 1-\alpha \\
P\left\{ -z_{\frac{\alpha}{2}} \le \frac{\sqrt{n}(\hat p - p)}{\sqrt{p(1-p)}}  \le z_{\frac{\alpha}{2}} \right\} &\approx 1-\alpha \\
P\left\{ -z_{\frac{\alpha}{2}} \le \frac{\hat p - p}{\sqrt{\frac{p(1-p)}{n}}}  \le z_{\frac{\alpha}{2}} \right\} &\approx 1-\alpha \\
P\left\{ -z_{\frac{\alpha}{2}}\sqrt{\frac{p(1-p)}{n}} \le \hat p - p \le z_{\frac{\alpha}{2}}\sqrt{\frac{p(1-p)}{n}} \right\} &\approx 1-\alpha \\
P\left\{\hat p-z_{\frac{\alpha}{2}} \sqrt{\frac{p(1-p)}{n}} \le p \le  \hat p + z_{\frac{\alpha}{2}} \sqrt{\frac{p(1-p)}{n}} \right\} &\approx 1-\alpha
\end{align}
$$
By Law of Large Number, $\hat p \to p$. 
Hence, we can use $\hat p$ to approximate $p$ when $n$ is large.
Then, the approximate $100(1-\alpha)\%$ CI is 
$$
\hat p \pm z_{\frac{\alpha}{2}} \sqrt{\frac{\hat p(1- \hat p)}{n}}
$$
Therefore, 
$$
\begin{align} \\
\hat p &\approx 0.527  \\
z_{0.025} &= 1.96\\ 
\text{Approximate $95\%$ CI for } p &= 0.527 \pm 1.96\sqrt{\frac{0.527(1-0.527)}{351}} \\
&= [0.475,0.579]
\end{align}
$$


To measure the difference in proportions between 2 independent populations,
> $p_i$: Proportion in population $i$ with a characteristic ($\frac{Y_i}{n_{i}}$)
> $Y_i$: No. of successes in sample from population $i$ 
> $n_i$: Sample size in population $i$

$$
\begin{align}
\mathbb E\left( \frac{Y_{i}}{n_{i}} \right) &= p_{i} \\
Var\left( \frac{Y_{i}}{n_{i}} \right) &= \frac{p_{i}(1-p_{i})}{n_{i}} 
\end{align}
$$
Hence, 
$$
\begin{align}
\mathbb E \left( \frac{Y_{1}}{n_{1}} - \frac{Y_{2}}{n_{2}}\right) &= p_{1} - p_{2} \\
Var\left( \frac{Y_{1}}{ n_{1}}  - \frac{Y_{2}}{n_{2}}\right) &= \frac{p_{1}(1-p_{1})}{n_{1}} + \frac{p_{2}(1-p_{2})}{n_{2}}
\end{align}
$$
When $n_1$ and $n_2$ is large, by CLT,
$$
\begin{align}
\hat p_{1} - \hat p_{2} &\sim N\left( p_{1} - p_{2}, \frac{p_{1}(1-p_{1})}{n_{1}} + \frac{p_{2}(1-p_{2})}{n_{2}} \right) \\
\frac{(\hat p_{1} - \hat p_{2}) - (p_{1} - p_{2})}{\sqrt{\frac{p_{1}(1-p_{1})}{n_{1}} + \frac{p_{2}(1-p_{2})}{n_{2}}}} &\sim N(0,1) \\
P\left\{ -z_{\frac{\alpha}{2}} \le \frac{(\hat p_{1} - \hat p_{2}) - (p_{1} - p_{2})}{\sqrt{\frac{p_{1}(1-p_{1})}{n_{1}} + \frac{p_{2}(1-p_{2})}{n_{2}}}} \le z_{\frac{\alpha}{2}}  \right\} &\approx 1-\alpha \\
\end{align}
$$
By Law of Large Number, we can approximate $p_i$ by $\hat p$. 
Hence, the approximate $100(1-\alpha)\%$ CI for $p_1 - p_2$ is 
$$
\hat p_{1} - \hat p_{2} \pm z_{\frac{\alpha}{2}} {\sqrt{\frac{\hat p_{1}(1- \hat p_{1})}{n_{1}} + \frac{\hat p_{2}(1-\hat p_{2})}{n_{2}}}}
$$
#### Example
> Let $p_{1}$ be the proportion of male students into gaming, and $p_2$ be the proportion of female students into gaming.
> Suppose $\hat p_1 = 0.6, \hat p_{2} = 0.4$.
> When $n_1 = 2000, n_2 = 2200$, please construct approximate 95% CI for $p_1 - p_2$.

The approximated 95% CI for $p_1 - p_2$ is given by
$$
\begin{align}
0.6-0.4 \pm z_{0.025} \sqrt{\frac{0.6(1-0.6)}{2000} + \frac{0.4(1-0.4)}{2200}} &= 0.2 \pm 1.96 \sqrt{\frac{0.6(0.4)}{2000} + \frac{0.4(0.6)}{2200}} \\
&= [0.17, 0.23]
\end{align}
$$
## Sample Size Determination
**动机：** 由于样本量多会增加成本，而样本量少会影响预测的准确度。因此我们需要找出在指定精度下，最少的样本量是多少。
### Normal Distribution ($\sigma^2$ Known)
For $X_1, \cdots, X_n \sim N(\mu, \sigma^2)$ and $\sigma^2$ is known, the $100(1-\alpha)\%$ CI for $\mu$ is 
$$
\bar x \pm z_{\frac{\alpha}{2}} \frac{\sigma}{\sqrt{n}}
$$
$z_{\frac{\alpha}{2}} \frac{\sigma}{\sqrt{n}}$ is called half-width, as well as **margin of error** or **max. error of the estimate**
> [!note]
> The smaller the half-width $z_{\frac{\alpha}{2}} \frac{\sigma}{\sqrt{n}}$, the more accurate the estimate.

We requires the half-width must be less than a given tolerance $\epsilon$ in precision
$$
\begin{align}
z_{\frac{\alpha}{2}} \frac{\sigma}{\sqrt{n}} &\le \epsilon \\
n &\ge \frac{z_{\frac{\alpha}{2}}^2\sigma^2}{\epsilon^2}
\end{align}
$$

#### Example
> A psychology study uses standardized memory tests with known standard deviation $\sigma = 12$.
> Find the minimum sample size $n$ needed for a 95% confidence interval with a margin of error at most 2.

$$
\begin{align}
n &\ge \frac{z_{0.025}^2 (12)^2}{2^2} \\
n &\ge 138.3
\end{align}
$$
Hence, the minimum sample size is 139 students.

### Normal Distribution ($\sigma^2$ Unknown)
When $\sigma^2$ is unknown, the $100(1-\alpha)\%$ CI is
$$
\bar x \pm t_{\frac{\alpha}{2}} (n-1) \frac{s}{\sqrt{n}}
$$
$t_{\frac{\alpha}{2}} (n-1) \frac{s}{\sqrt{n}}$ is the half-width.
Hence, 
$$
\begin{align}
t_{\frac{\alpha}{2}} (n-1) \frac{s}{\sqrt{n}} &\le \epsilon \\
n &\ge  \frac{t^2_{\frac{\alpha}{2}} (n-1) s^2}{\epsilon^2}
\end{align}
$$
However, there are 2 issues
- $t^2_{\frac{\alpha}{2}} (n-1)$ depends on $n$. Hence, we use $z_\frac{\alpha}{2}$ to approximate $t^2_{\frac{\alpha}{2}} (n-1)$
- $s^2$ depends on $n$. Hence, we have to estimate $s^2_p$ from prior knowledge / pilot study
Finally,
$$
n\ge \frac{z^2_{\frac{\alpha}{2}} (s^2_{p})}{\epsilon ^2}
$$

### Proportion
The approximate CI for proportion $p$ is 
$$
\hat p \pm z_{\frac{\alpha}{2}} \sqrt{\frac{\hat p(1-\hat p)}{n}}
$$

Let the required precision be $\epsilon$.
$$
\begin{align}
z_{\frac{\alpha}{2}} \sqrt{\frac{\hat p(1-\hat p)}{n}} &\le \epsilon \\
n &\ge \frac{ z^2_{\frac{\alpha}{2}}\ \hat p (1-\hat p)}{\epsilon^2}
\end{align}
$$
However, $\hat p$ depends on $n$
Since $\hat p$ is unknown, we have 2 approach to approximate $\hat p$
- Use prior estimate $p^*$:
	- 来自历史数据、以前的调查或者预试研究（pilot study）
$$
n \ge \frac{ z^2_{\frac{\alpha}{2}}\ p^* (1-p^*)}{\epsilon^2}
$$
- Use the max. variance
	- As $p\in [0,1]$, $p(1-p)\le \frac{1}{4}$
	- $p(1-p)$ attains its maximum when $p=\frac{1}{2}$
	- Hence, assume $\hat p = \frac{1}{2}$
$$
\begin{align}
n &\ge \frac{z^2_{\frac{\alpha}{2}} \frac{1}{2}\left( 1-\frac{1}{2} \right)}{\epsilon^2} \\
&\ge \frac{z^2_{\frac{\alpha}{2}}}{4\epsilon^2}
\end{align}
$$
> [!note] Proof
> **Prove $p(1-p)\le \frac{1}{4}$ by completing square.**
> $$
> \begin{align}
>  p(1-p)&= p-p^2,\quad p\in [0,1] \\
>  &= -\left( p^2-p+\frac{1}{4} \right) +\frac{1}{4}\\
>  &= -\left( p - \frac{1}{2} \right)^2 + \frac{1}{4} \\
>  \therefore p(1-p) \text{ attains its maximum at }&\left( \frac{1}{2}, \frac{1}{4} \right)
> \end{align}
> $$

#### Example
> A particular area contains 8000 apartment units.
> In a preliminary survey, 12% of the respondents said they planned to sell their apartments within the next year.
> We want to estimate the interval for the total number of owners planning to sell.
> Suppose that a 95% confidence interval with the half-width less than 200 is desired. How many owners do we need to survey.

From now, we have
- $p^*$: 12% (it is prior estimate)
- $\epsilon$: 200
- $\alpha$: 5%
As there are 8000 apartments in total, the approximate CI of the number of owners planning to sell has to multiply by 8000.
$$
\begin{align}
8000 \left(z_{0.025} \sqrt{\frac{\hat p(1-\hat p)}{n}}\right) &\le 200 
\end{align}
$$
Approximate $\hat p$ by $p^*$
$$
\begin{align}
8000 \left(1.96\sqrt{\frac{0.12(1-0.12)}{n}}\right) &\le 200 \\
1.96\sqrt{\frac{0.1056}{n}} &\le 0.025\\
n &\ge 649.077
\end{align}
$$
Hence, we need to survey at least 650 apartment owners