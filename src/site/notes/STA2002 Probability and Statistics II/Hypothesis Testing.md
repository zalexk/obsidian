---
{"dg-publish":true,"permalink":"/sta-2002-probability-and-statistics-ii/hypothesis-testing/","created":"2026-10-08T16:38:49.693+08:00","updated":"2026-10-13T01:56:02.007+08:00","dg-note-properties":{}}
---


## Concepts
### Null Hypothesis $H_0$ and Alternative Hypothesis $H_1$
- **Null hypothesis $H_0$:** Initial claim / assumption on the values that $\mu$ can take
	- 通俗来说：没变化 / 维持现状
- **Alternative hypothesis $H_1$:** The competing claim / assumption against which we would like to test the initial claim / assumption
	- 通俗来说：想证明的新发现
> [!tip]
> 判决要么是"**reject / retain 拒绝 $H_0$ **"，要么是"**fail to reject 未能拒绝 $H_0$ **"，而**不是"接受 $H_0$"**。
- **Simple hypothesis:** Hypothesis in which $\mu$ only takes on 1 value
- **Composite hypothesis:** Hypothesis in which $\mu$ takes on a range of value

#### Example
> Let $X$ equal the breaking strength of a steel bar. 
> If the bar is manufactured by process I, $X\sim N(50,36)$. 
> It is **hoped** that if process II (a new process) is used, $X\sim N(55,36)$. 
> Given a large number of steel bars manufactured by process II, how could we test whether the five-unit increase in the mean breaking strength was realized?

**Judgement:** 5-unit increase in $\mu$  or not
- **Simple null hypothesis $H_0$:** $\mu = 50$
- **Simple alternative hypothesis $H_1$:** $\mu = 55$
- **Composite null hypothesis $H_0$:** $\mu \le 50$
- **Composite alternative hypothesis $H_1$:** $\mu >55$

| $H_0$        | $H_1$        | Types                  | 直觉解释           |
| ------------ | ------------ | ---------------------- | -------------- |
| $\mu = 50$   | $\mu = 55$   | Simple vs Simple       | 只关心两个精准数值      |
| $\mu = 55$   | $\mu > 55$   | 单侧 One-sided（右尾）       | 只关心"**有没有变大**" |
| $\mu = 55$   | $\mu < 55$   | 单侧 One-sided（左尾）       | 只关心"**有没有变小**" |
| $\mu = 55$   | $\mu \ne 55$ | 双侧 One-sided（双尾）       | 变大变小**都算异常**   |
| $\mu \le 55$ | $\mu > 55$   | Composite vs Composite | 覆盖全部数值         |

### Critical Region $C$ and Test Statistic $T$
The space of the sample $\mathcal{D} := \{(x_1, x_2, \ldots, x_n) \mid x_i \in S_X,\ i = 1,2,\cdots,n\}$ 
> [!tip]
> $\mathcal D$: 这次抽样所有可能出现的结果的 set

Hypothesis testing is based on critical region $C$, which is subset of $\mathcal D$.
- Reject $H_0$ (accept $H_1$) if $(x _1,x_ 2,\cdots,x_n) \in C$
- Fail to reject $H_0$ (reject $H_1$) if $(x _1,x_ 2,\cdots,x_n) \notin C$
> [!tip]
> **临界域 $C$ 是 $\mathcal{D}$ 的一个子集：**只要实际抽到的样本落在 $C$ 里，就拒绝原假设 $H_0$（null hypothesis）；没落在里面，就不拒绝。
> $$
> \text{样本} \in C \;\Rightarrow\; \text{拒绝 } H_0 \qquad \text{样本} \notin C \;\Rightarrow\; \text{不拒绝 } H_0
> $$

Test statistic $T$ is quantity derived from the sample for hypothesis testing.
> [!tip]
> $T$ 是一个"摘要函数"，把 $n$ 个数据压缩成一个数。
> **类比：** 想知道一个班学得好不好，不用逐一报 50 个人的分数，只看"平均分"这一个数就够了。平均分就是一个统计量 statistic。

The critical region $C$ is usually specified in terms of test statistic $T$.

In the [[STA2002 Probability and Statistics II/Hypothesis Testing#Example\|#Example]], 
- Test statistic $T = \bar X$
- Critical region $C = \{(x_1,x_2,\cdots,x_n)\in\mathcal{D} \mid \bar{x}\ge 53\}$
### Errors in Hypothesis Testing
|                      | $H_0$ true   | $H_1$ true    |
| -------------------- | ------------ | ------------- |
| Reject $H_0$         | Type I error | Correct       |
| Fail to Reject $H_0$ | Correct      | Type II Error |

- **Type I error:** False positive 误报
$$
\alpha = P(\text{Type I error}) = P(T\in C; H_{0})
$$
- **Type II error:** False negative 漏报
$$
\beta = P(\text{Type II error}) = P(T\notin C; H_{1})
$$

|                   | 真的没病（$H_0$）               | 真的有病（$H_1$）               |
| ----------------- | ------------------------- | ------------------------- |
| 报告"阳性"（拒绝 $H_0$）  | 误报（false positive）= 第一类错误 | 命中                        |
| 报告"阴性"（不拒绝 $H_0$） | 命中                        | 漏报（false negative）= 第二类错误 |

#### Example
> $X_1, \dots, X_n \overset{i.i.d.}{\sim} N(\mu, 36)$，$n=16$
> Take critical region $C = \{ \bar x \ge 53 \}$.
> What is the probability of type I error and type II error in the following test
> $$
H_0: \mu = 50 \quad \text{against} \quad H_1: \mu = 55
$$

$$
\begin{align}
\bar X &\sim N\left( \mu, \frac{\sigma^2}{n}\right) \\
&\sim N\left( \mu, \frac{36}{16} \right) \\ 
&\sim N(\mu, 2.25)\\
\alpha &= P(\bar X \ge 53; \mu = 50)  \\
&=P\left( Z \ge \frac{53-50}{\sqrt{2.25}} \right) \\
&= P(Z \ge 2) \\
&\approx 0.0228
\end{align}
$$
> [!tip]
> 哪怕真实均值就是 50，单凭抽样波动，也有约 2.28% 的概率 $\bar{x}$ 在 53 以上，被我们冤枉。
$$
\begin{align}
\beta &= P(\bar X < 53; \mu = 55) \\
&= P\left( Z< \frac{53-55}{\sqrt{2.25}} \right) \\
&= P(Z < -1.333) \\
&\approx 0.0912
\end{align}
$$
> [!tip]
> 即便真实均值是 55，仍有约 9.12% 的概率没跨过 53 而漏报

![Error in Hypothesis Testing.png](/img/user/%E9%99%84%E4%BB%B6/Error%20in%20Hypothesis%20Testing.png)

> [!note]
> By changing critical region $C$, $\alpha$ and $\beta$ change in different direction (i.e. $\alpha \uparrow \beta \downarrow$).
> Hence, $\alpha$ and $\beta$ cannot be reduced at the same time


### Significance Level
We usually fix the probability of type I error $\alpha$, and then determine the corresponding critical region.
In this scenario, the value of $\alpha$ is called significance level of the test.
> [!tip]
> 在先确定 type I error $\alpha$ 的值，再决定 critical region 的情景下，$\alpha$ 便称为 significance level

#### Example
> $X_1, \dots, X_n \overset{i.i.d.}{\sim} N(\mu, 36)$，$n=16$
> Take $\alpha = 0.05$
> Find the critical region
$$
\begin{align}
\Pr\left( Z \ge \frac{c-50}{\sqrt{2.25}} \right) &= 0.05 \\
\frac{c-50}{\sqrt{2.25}} &= z_{0.05} \\
c &= 52.48
\end{align}
$$

> [!note]
> $$
> \Pr(Z \ge z_\alpha) = \alpha
> $$

> [!note]
> 注意权衡（Trade-off）：$\alpha$ 调小 → 拒绝域变小 → 第一类错误减少，但第二类错误 $\beta$（放过坏人）会增大。$\alpha$ 和 $\beta$ 像跷跷板，样本量 $n$ 不变时无法同时减小。

> [!caution] 常见误区提醒
> - $\alpha = 0.05$ 不是"$H_0$ 有 5% 的概率为真"，而是"假如 $H_0$ 为真，我们错误拒绝它的概率是 5%"。  
> - $z_{0.05}$ 的记号指右尾面积为 0.05，查表时别和 $\Phi(z)=0.05$（左尾）搞混。因为 $\Phi(1.645) = 0.95$，所以右尾才是 0.05。  
> - 拒绝域方向由 $H_1$ 决定：$H_1: \mu > 50$ → 右尾；$H_1: \mu < 50$ → 左尾；$H_1: \mu \ne 50$ → 双尾（$\alpha$ 平分两边）。
> ![Normal distribution in left and right tail.png](/img/user/%E9%99%84%E4%BB%B6/Normal%20distribution%20in%20left%20and%20right%20tail.png)

### $p$-value: Observed Significance Level
**$p$-value:** If $H_0$ is true, the probability of observing a more extreme test statistic (favour $H_1$)
Smaller $p$-value indicates the data is more unlikely coming from $H_0$ and $H_1$ is perhaps better retained

> [!tip]
>   
> 想象一个场景：你抛一枚硬币 100 次，得到 90 次正面。你会怀疑硬币是不是被做手脚了（$H_0$: 硬币公平 vs $H_1$: 硬币不公平）。  
> - $p$-value = 0.0001 的意思是：如果硬币真的公平，100 次里得到 90 次正面（或更极端）的概率只有 0.01%。  
> - 这个概率太小了，所以我们有理由怀疑硬币不公平。

$H_0$ is rejected if $p$-value $\le \alpha$
#### Example
Following the same example above ($\sigma^2 = 36$，$n = 16, \alpha = 0.05$).
Given observed test statistics $\bar x = 56$.
- For $H_0 : \mu = 50$ versus $H_1:\mu = 55$
	- 更极端方向是 $\bar X \ge 56$
$$
\begin{align}
\Pr\left( Z \ge \frac{56-50}{\sqrt{2.25}} \right) &= \Pr(Z\ge 4) \\
&= 0.00003 \\
&\le \alpha \\
\therefore H_{0} &\text{ is rejected}
\end{align}
$$
- For $H_0 : \mu = 55$ versus $H_1: \mu > 55$
	- 更极端方向是 $\bar X \ge 56$
$$
\begin{align}
\Pr\left( Z\ge \frac{56-55}{\sqrt{2.25}} \right) &= 0.2525 \\
&\ge \alpha 
\end{align}
$$
- For $H_0: \mu = 55$ versus $H_1: \mu < 55$
	- 更极端方向是 $\bar X \le 56$
$$
\begin{align}
\Pr\left( Z \le \frac{56-55}{\sqrt{2.25}} \right) &= 0.7475 \\
&\ge \alpha
\end{align}
$$
- For $H_0: \mu = 55$ versus $H_1: \mu \ne 55$
	- 更极端方向是 $\bar X\ge 56$ and $\bar X \le 54$
$$
\begin{align}
\Pr\left( Z\ge \frac{56-55}{\sqrt{2.25}} \right) + \Pr\left( Z\le \frac{54-55}{\sqrt{2.25}} \right) &= P(Z\ge 0.667) + P(Z \le -0.667) \\
&\approx 0.505 \\
&\ge \alpha
\end{align}
$$
## Hypothesis Testing for Normal Mean
There are 3 approaches to hypothesis testing
- $p$-value approach
	- Reject $H_0$ if $p$-value $\le \alpha$
- Critical region approach
	- Reject $H_0$ if statistic falls in critical region
- Confidence interval approach
	- Reject $H_0$ if null value (value of null hypothesis) is not include in CI
### Case 1: $\sigma^2$ Known
Consider test statistic 
$$
T:= \frac{\bar X - \mu_0}{\frac{\sigma}{\sqrt{n}}}
$$
Under $H_0:\mu = \mu_{0}$, $T\sim N(0,1)$
> [!tip]
> 1.  $\mu_0$ 只是一个已知的、假设的数值。
> 2. 当 $T$ 被定义为 $\frac{\bar X - \mu_0}{\frac{\sigma}{\sqrt{n}}}$，由于 $\mu$ 并未假设为 $\mu_{0}$，因此 $T\nsim N(0,1)$。
> 3. 直到题目给出 "Under $H_0:\mu = \mu_{0}$"，假定 $\mu$ 为 $\mu_{0}$ 时，$T$ 才服从 $N(0,1)$。

Once the data $x_1, \cdots, x_n$ is observed, we can compute
$$
z = \frac{\bar x - \mu_{0}}{\frac{\sigma}{\sqrt{n}}}
$$
> [!tip]
> $z$ is observed value of $T$

> [!important]
> - 大写 = 随机变量（random variable）
> - 小写 = 观测值（observed value / realization）

**For the one-sided test** $H_0:\mu = \mu_0,\ H_1: \mu \boxed{>} \mu_0$
- $p$-value is
$$
\begin{aligned}
p = \Pr(T>z; H_{0}) = \Pr(Z>z)
\end{aligned}
$$
- Reject $H_0$ when either
	- **$p$-value approach:** $p\le \alpha$ OR
	- **Critical region approach:** $z\ge z_\alpha$ OR
	- **Confidence interval approach:** $\mu_0 \notin \left( \bar x - z_{\alpha} \frac{\sigma}{\sqrt{n}}, \infty \right)$
> [!tip]
> 这三种 approach 都是等价的

**For one-sided test** $H_0:\mu = \mu_0,\ H_1:\mu \boxed{<} \mu_0$
$$
p = \Pr(T< z;H_{0}) = \Pr(Z<z)
$$
Reject $H_0$ when either
- $p\le \alpha$ OR
- $z\le - z_\alpha$ OR
- $\mu_{0} \notin \left( -\infty, \bar x + z_{\alpha}\frac{\sigma}{\sqrt{n}} \right)$
**For two-sided test** $H_0: \mu = \mu_{0}, \ H_{1} : \mu \ne \mu_{0}$
$$
\begin{aligned}
p &= \Pr(|T| > |z|; H_{0}) \\
&= \Pr(Z>|z|) + \Pr(Z<|z|) \\
&=2\Pr(Z>|z|) 
\end{aligned}
$$
Reject $H_0$ when either
- $p\le\alpha$ OR
- $|z| \ge z_{\frac{\alpha}{2}}$ OR
- $\mu_0 \notin \left( \bar x - z_{\frac{\alpha}{2}} \frac{\sigma}{\sqrt{n}}, \bar x + z_{\frac{\alpha}{2}} \frac{\sigma}{\sqrt{n}}\right)$
![z-curve.png](/img/user/%E9%99%84%E4%BB%B6/z-curve.png)
### Case 2: $\sigma^2$ Unknown
When $\sigma^2$ is unknown, replace standard normal distribution by $t$-distribution with degree of freedom $(n-1)$ and $\sigma^2$ by $S^2$ in [[STA2002 Probability and Statistics II/Hypothesis Testing#Case 1 $ sigma 2$ Known\|#Case 1 $ sigma 2$ Known]]

Consider test statistic 
$$
T:=\frac{\bar X - \mu_{0}}{\frac{S}{\sqrt{n}}}
$$
Under $H_0:\mu = \mu_0$, $T\sim t(n-1)$
Once data $x_1,\cdots, x_n$ are observed, we can compute
$$
t = \frac{\bar x - \mu_{0}}{\frac{s}{\sqrt{n}}}
$$
**For the one-sided test** $H_0 :\mu = \mu_0, \ H_1:\mu \boxed> \mu_0$
$$
p = \Pr(T>t; H_{0}) = \Pr(T>t; T\sim t(n-1))
$$
Reject $H_0$ when either
- $p\le \alpha$ OR
- $t\ge t_{\alpha} (n-1)$ OR
- $\mu_0 \notin \left( \bar x - t_{\alpha}(n-1) \frac{s}{\sqrt{n}}, \infty \right)$
**For the one-sided test** $H_0:\mu=\mu_ 0, \ H_1 : \mu \boxed<\mu_0$
$$
p = \Pr(T<t; T\sim t(n-1))
$$
Reject $H_0$ when either
- $p\le \alpha$ OR
- $t\le - t_\alpha (n-1)$
- $\mu_0\notin \left( -\infty, \bar x + t_{\alpha}(n-1) \frac{s}{\sqrt{n}}\right)$
**For the one-sided test** $H_0 : \mu = \mu_0, \ H_1:\mu \ne \mu_0$
$$
\begin{aligned}
p &= \Pr(|T|>|t|; H_{0}) \\
&= \Pr(T>|t|; T\sim t(n-1)) + \Pr(T<-|t|; T\sim t(n-1)) \\
&= 2\Pr(T>|t|; T\sim t(n-1))
\end{aligned}
$$
Reject $H_0$ when either
- $2\Pr(T>|t|; T\sim t(n-1))\le \alpha$
- $|t|\ge t_{\frac{\alpha}{2}} (n-1)$
- $\mu_0 \notin \left( \bar x - t_{\frac{\alpha}{2}}(n-1) \frac{s}{\sqrt{n}}, \bar x + t_{\frac{\alpha}{2}}(n-1) \frac{s}{\sqrt{n}} \right)$
#### Example
##### Two-sided Test
> Let $X$ (in millimeters) equal the growth in 15 days of a tumor induced in a mouse.
> Assume that the distribution of $X$ is $N(\mu, \sigma^2)$
> Test the null hypothesis $H_0:\mu = 4.0$ against the two-sided alternative hypothesis $H_1:\mu\ne 4.0$
> Observe that $n=9$ observations with $\bar x = 4.3, s= 1.2$ and set significance level of $\alpha = 0.10$

$$
\begin{aligned}
t &= \frac{4.3-4}{\frac{1.2}{\sqrt{9}}} = 0.75 \\
t_{\frac{0.10}{2}}(9-1) &= t_{0.05}(8) \\
&= 1.86 \\
\text{$p$-value approach: }p&= 2\Pr(T>0.75; T\sim t(8)) \\
&= 0.4747 \\
&>0.1 \\
\text{Critical region approach: } |t| &= 0.75  \\
&\le 1.86 \\
\text{Confidence interval approach: } 4.3\pm 1.86\left( \frac{1.2}{\sqrt{9}} \right) &= [3.556, 5.044] \\
4 &\in [3.556, 5.0044]
\end{aligned}
$$
Hence, we fail to reject $H_0$ at 10% significance level

##### One-sided Test
> Suppose that we have $n=25, \bar x = 308.8, s=115.15$
> Test $H_0:\mu=500$ against $H_1:\mu<500$, given significance level $\alpha = 0.01$

$$
\begin{aligned}
t &= \frac{308.8-500}{\frac{115.15}{\sqrt{25}}} \\
&= -8.30  \\
t_{0.01}(24) &= 2.492 \\
\text{$p$-value approach: }p&= \Pr(T<-8.30;T\sim t(24)) \\
&= 8.17\times 10^{-9} \\
&<0.01 \\
\text{Critical region approach: } t&=-8.30 \\
&< -2.492 \\
\text{Confidence interval approach: The 99\% one-sided CI is} &\left( -\infty, 308.8+2.492 \times \frac{115.15}{\sqrt{25}} \right) \\
&= (-\infty, 366.191)
\end{aligned}
$$

![Hypothesis testing for one mean.png](/img/user/%E9%99%84%E4%BB%B6/Hypothesis%20testing%20for%20one%20mean.png)