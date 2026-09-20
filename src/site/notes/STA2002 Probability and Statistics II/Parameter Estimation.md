---
{"dg-publish":true,"permalink":"/sta-2002-probability-and-statistics-ii/parameter-estimation/","created":"2026-09-15T00:18:08.693+08:00","updated":"2026-09-20T18:14:57.817+08:00","dg-note-properties":{}}
---


## Data Visualization
Histogram is used to visualize continuous observations by grouping data into several bins
- **Height:** Relative frequency / density of data points
	- **Relative frequency:** $\frac{\text{\# of data in the bin}}{\text{\# of total data}}$
	- **Density:** $\frac{\text{Relative frequency}}{\text{Bin width}}$
	- Let there are $k$ bins,  the bin width of $j$ be $w_j$, and the number of data observed in the bin is $n_j$.
		- Relative frequency = $\frac{n_j}{n}$
		- Density = $\frac{n_j}{w_j n}$
			- Sum of areas of all bins always equal to 1: $\sum_{j=1}^k w_j \left(\frac{n_j}{w_j n} \right)= 1$
	- ![histogram.png](/img/user/%E9%99%84%E4%BB%B6/histogram.png)
- **Area:** Proportional to the num. of observations 
In PDF, probability is the area under the density curve. 
Histogram is the discrete version for PDF.

The bin size (num. of bins) is important
- **Too small:** Overfit
- **Too large:** Hide important details & patterns in the data
### Boxplot

$$
\min, \overbrace{\underbrace{Q_1}_\frac{1}{4}, \underbrace{Q_2}_{\text{median}}, \underbrace{Q_3}_\frac{3}{4}}^{\text{Interquartile range}}, \max
$$
![boxplot.png](/img/user/%E9%99%84%E4%BB%B6/boxplot.png)
- IQR = $Q_3-Q_ 1$
- Fence
	- **Inner fence:** Left /right of box at distance $(1.5\times IQR)$
	- **Outer fence:** Left / right of box at distance $(3\times IQR)$
- Whisker
	- **Lower whisker:** From $Q_1$ down to the smallest observation $\ge Q_1 - 1.5 \times IQR$
	- **Upper whisker:** From $Q_3$ up to the largest observation $\le Q_3 + 1.5 \times IQR$
- **Suspect outlier:** Between inner & outer fence $(Q_{3} + 3 \times IQR > x > Q_{3} + 1.5 \times IQR)$ or $(Q_{1}-3\times IQR< x < Q_{1}-1.5 \times IQR )$
- **Outlier:** Beyond the outer fence ($x>Q_{3} + 3 \times IQR$ or $x<Q_{1}-3\times IQR$ )
#### Interpretation
- Box shows the middle 50% of data
- Whiskers show the range of normal data points
	- i.e. data within $\pm 1.5\times IQR$ are normal
	- **Left-skewed:** Lower whisker is longer than upper whisker
	- **Right-skewed:** Upper whisker is longer than lower whisker
- Data beyond outer fence are outliers
- Boxplot shows the variance & skewness of data + identify outliers

---
## Parameter Estimation / Point Estimation
Given a sample with size $n$ from population
Assumption:
- Sample is representative of the population
- Data are i.i.d.
### Parameter Space
Suppose sample $X_1, \cdots, X_n$ are random and i.i.d. with unknown parameter $\theta$ and PMF / PDF $f(x;\theta)$.
The parameter $\theta$ takes value in the parameter space $\Omega$ (i.e. domain of $\theta$)
> [!note]
> 在之后求解 MLE 时起到硬约束的作用（不可以取超过 $\Omega$ 的值）


> **Example**
> For the PDF of normal distribution,
> $$
f(x) = \frac{1}{\sigma \sqrt{2\pi}} \exp \left[ -\frac{(x-\mu)^2}{2\sigma^2}\right], \quad -\infty < x < \infty
$$
> Hence, the corresponding parameter space is
> $$
\Omega = \{ (\mu, \sigma^2): -\infty < \mu < \infty, 0<\sigma^2 < \infty \}
$$
> $\mu$ 可以取任意 real number
> $\sigma^2$ 必然是 positive number，必然大于 0

### Estimator
| 写法       | 名称                    | 性质                    | 例子             |
| -------- | --------------------- | --------------------- | -------------- |
| 大写 $X_i$ | 随机变量（random variable） | 在抽样**之前**，结果是未知的，是随机的 | "下一位被测者的身高"    |
| 小写 $x_i$ | 观测值（observed value）   | 抽样**之后**，已经拿到手的确定数值   | 我实际测到 172.5 cm |
- **Estimator of $\theta$:**  $\hat \theta = u(X_1,X_ 2, \cdots, X_n)$
- **Estimate of $\theta$:** Value of  $u(x_1,x_ 2, \cdots, x_n)$
Since $u(X _1,X_ 2, \cdots, X_n)$  outputs a single value, it is called a point estimator
$$
\underbrace{u(X_1,\ldots,X_n)}_{\text{Point estimator：Random variables}}
\ \xrightarrow{\ \text{代入具体样本}\ }\
\underbrace{u(x_1,\ldots,x_n)}_{\text{point estimate：Single value}}
\ \xrightarrow{\ \text{用来猜}\ }\
\underbrace{\theta}_{\text{真参数：永远不知道}}
$$
#### Evaluate estimate
- **偏差 Bias:** $\text{Bias}(\hat\theta) = E(\hat\theta) - \theta$
- **Variance:** $\operatorname{Var}(\hat\theta) = E\!\left[\left(\hat\theta - E\hat\theta\right)^2\right]$
- **Mean square error (MSE):** $\underbrace{E\!\left[(\hat\theta-\theta)^2\right]}_{\textbf{总误差 MSE}}= \underbrace{\operatorname{Var}(\hat\theta)}_{\textbf{抖（精度）}}+ \underbrace{\left[E(\hat\theta)-\theta\right]^2}_{\textbf{偏（准确度）}}$
- **Consistency:** $\lim_{n\to\infty}\Pr\left(\left|\hat\theta - \theta\right| > \varepsilon\right) = 0$
	- 评估样本多了会不会变好
### Maximum Likelihood Estimation
#### Estimator
$$
\begin{align}
L(\theta) &:= f(x_1, x_2, \cdots, x_n;\theta) = \prod_{i=1}^{n} f(x_i;\theta) \\
\ell(\theta) &:= \ln L(\theta)
\end{align}
$$

$L(\theta) \to \ell (\theta)$  使得乘积变成求和，方便求导计算

**Maximum likelihood estimator (MLE) $\hat \theta$:** Value of $\theta$ that maximizes $L(\theta)$ 
$$
\hat\theta = \arg\max_{\theta \in \Omega} L(\theta)
$$
#### Calculation of MLE
1. Formulate $\ell(\theta)$
2. $\underbrace{\frac{\partial \ell(\theta)}{\partial \theta}}_{\text{score function}} = 0 \Rightarrow \hat \theta$
	1. 这一步的 $\hat \theta$ 只是 stationary point，不一定是 maximum point
3. $-\left.\dfrac{\partial^2 \ell(\theta)}{\partial \theta^2}\right|_{\theta = \hat\theta} > 0 \Rightarrow \hat\theta \text{ is MLE}$
#### Example
##### Bernoulli Distribution
1. Formulate $\ell(\theta)$
$$
\begin{align}
f(x;p) &= p^x (1-p)^{1-x}, \quad x\in\{0,1\}, \quad 0\le p \le 1\\
L(p) &= \prod_{{i=1}}^n p^{x_{i}} (1-p)^{1-x_{i}} \\
&= p^{\sum_{i=1}^n x_{i}} (1-p)^{\sum_{i=1}^n 1-x_{i}} \\ \\
&= p^{\sum_{i=1}^n x_{i}} (1-p)^{n-\sum_{i=1}^n x_{i}}\\
\ell (p) &= \left(\sum_{i=1}^n x_{i}\right)\ln p + \left(n-\sum_{i=1}^n x_{i} \right) \ln(1-p)
\end{align}
$$
2. Use score function to find MLE
$$
\begin{align}
\ell'(p) &= 0 \\
\left(\sum_{i=1}^n x_{i}\right) \frac{1}{p} - \left(n-\sum_{i=1}^n x_{i} \right) \frac{1}{1-p} &= 0 \\
\left(\sum_{i=1}^n x_{i}\right) \frac{1}{p} &= \left(n-\sum_{i=1}^n x_{i} \right) \frac{1}{1-p} \\
(1-p)\left(\sum_{i=1}^n x_{i}\right)&= p\left(n-\sum_{i=1}^n x_{i} \right)\\
\sum_{i=1}^n x_{i}-p\sum_{i=1}^n x_{i} &= pn -p\sum_{i=1}^n x_{i} \\
\sum_{i=1}^n x_{i}&= pn \\
p &= \frac{1}{n} \sum_{i=1}^n x_{i} \\
\hat p &= \bar x
\end{align}
$$
3. Verify $\hat \theta$ is MLE
$$
\begin{align}
\ell''(p) &= -\frac{\sum_{i=1}^n x_{i}}{p^2} - \left(n-\sum_{i=1}^n x_{i} \right) \frac{1}{(1-p)^2} \\
\because \sum_{i=1}^n x_{i} \ge 0&,\quad n-\sum_{i=1}^n x_{i} \ge 0 \\
\ell''(p) &< 0
\end{align}
$$
Since $\ell''(p)<0$, $\ell(p)$ is strictly concave function, $\hat p = \bar x$ is the MLE.
The MLE is the sample mean in Bernoulli Distribution.
##### Exponential Distribution
$$
\begin{align}
f(x;\theta) &= \frac{1}{\theta}e^{-x/\theta}, \quad 0 < x < \infty, \quad \theta \in (0,\infty) \\
L(\theta) &= \frac{1}{\theta^n} \exp \left(-\frac{\sum_{i=1}^n x_{i}}{\theta} \right) \\
\ell (\theta) &= -\frac{\sum_{i=1}^n x_{i}}{\theta}+ \ln \frac{1}{\theta^n} \\
&=-\frac{\sum_{i=1}^n x_{i}}{\theta} - n\ln \theta \\ \\

\ell '(\theta) &= 0 \\ 
\frac{\sum_{i=1}^n x_{i}}{\theta^{2}} - \frac{n}{\theta} &= 0 \\
\frac{\sum_{i=1}^n x_{i}}{\theta^{2}} &= \frac{n}{\theta}  \\
\theta &= \frac{1}{n}\sum_{i=1}^n x_{i} \\
\hat \theta &= \bar x \\
 \\
\ell''(\theta) &= -\frac{2\sum_{i=1}^n x_{i}}{\theta^{3}} + \frac{n}{\theta^2} \\ 
&= -\underbrace{\frac{2n\bar x}{\theta^3}}_{\bar x = \frac{1}{n}\sum_{i=1}^n x_{i}} + \frac{n}{\theta^2}\\
\ell''(\theta) \big|_{\theta = \bar x} &= -\frac{2n \bar x}{\bar x^3} + \frac{n}{\bar x^2} \\
&= -\frac{2n}{\bar x^2} + \frac{n}{\bar x^2} \\
&= -\frac{n}{\bar x^2} \\
&<0
\end{align}
$$
Hence, $\hat \theta = \bar x$ is the MLE for Exponential Distribution.

##### Poisson Distribution
$$
\begin{align}
 f(x; \lambda) &= \frac{\lambda^{x}}{x!} e^{-\lambda} \\
 L(\lambda) &= \prod_{i=1}^n \frac{\lambda^{x_{i}}}{x_{i}!} e^{-\lambda} \\
 &= \frac{\lambda^{\sum_{i=1}^n x_{i}}}{\prod_{i=1}^n x_{i}!}e^{-n\lambda} \\
 \ell (\lambda) &= \sum_{i=1}^n x_{i}\ln \lambda - \ln \left(\prod_{i=1}^n x_{i}! \right) - n\lambda \\ \\
 \ell'(\lambda)&=\frac{1}{\lambda}\sum_{i=1}^n x_{i}-n \\
 0 &= \frac{n\bar x}{\lambda} - n \\
 n\lambda &= n\bar x \\
 \hat \lambda &= \bar x \\ \\
 -\ell''(\lambda) &= \frac{1}{\lambda^2}\sum_{i=1}^n x_{i} \\
 -\ell''(\lambda)\big | _{\lambda = \bar x} &= \frac{1}{\bar x^2}\sum_{i=1}^n x_{i} \\ 
 &= \frac{1}{\bar x^2 } n\bar x \\
 &= \frac{n}{\bar x} \\
 &>0
\end{align}
$$
##### Geometric Distribution
$$
\begin{align}
f(x; p) &= (1-p)^{x - 1}p \\
L(p) &= \prod^n_{{i=1}} (1-p)^{x_{i} - 1} p \\
&= (1-p)^{\sum_{i=1}^n x_{i} - n}p^n \\
\ell(p) &= \left(\sum_{i=1}^n x_{i} - n \right) \ln (1-p) + n\ln p \\ \\
\ell'(p) &= 0 \\
0 &= -\frac{1}{1-p} \left(\sum_{i=1}^n x_{i} - n \right) + \frac{n}{p} \\
\frac{n\bar x - n}{1-p} &= \frac{n}{p} \\
\frac{\bar x - 1}{1-p} &= \frac{1}{p} \\
p(\bar x - 1) &= 1-p \\
p\bar x &= 1 \\
\hat p &= \frac{1}{\bar x} \\ \\

-\ell''(p) &= \frac{1}{(1-p)^2}\left(\sum_{i=1}^n x_{i} - n \right) + \frac{n}{p^2} \\
&= \frac{1}{(1-p)^2}\left(n\bar x - n \right) + \frac{n}{p^2} \\
-\ell''(p) \big|_{p = \frac{1}{\bar x}}&= \frac{1}{\left( 1-\frac{1}{\bar x} \right)^2}\left(n\bar x - n \right) + \frac{n}{\frac{1}{\bar x^2}} \\
&= \frac{\bar x^2 (n\bar x - n)}{(\bar x - 1)^2} + \bar x^2 n \\
&= \frac{n\bar x^2 (\bar x-1)}{(\bar x - 1)^2} + \bar x^2 n \\
&= n\bar x^2 \left[\frac{\bar x-1}{(\bar x - 1)^2} + 1 \right] \\
&> 0
\end{align}
$$
##### Uniform Distribution (Special Cases)
$$
\begin{align}
f(x) &= \begin{cases}
\frac{1}{\theta}, \quad 0 \le x\le \theta, \\
0, \quad \text{Otherwise}
\end{cases}  \quad \theta \in (0,\infty)
\end{align}
$$
For the likelihood function $L(\theta)$,
$$
L(\theta) = \prod_{i=1}^n f(x_{i};\theta)
$$
If $x_i > \theta$ or $x_{i} < 0$, then $f(x_i) = 0$ and $L(\theta)= 0$
Hence, $L(\theta) >0 \iff$ 
- $0\le \min_i x_i$ and
- $\max\{x_1, x_2, \cdots, x_n\}\le \theta$
$$
L(\theta) = \begin{cases}
\frac{1}{\theta^{n}}, \quad &\theta \ge \max_{i} x_{i} \\
0, \quad &\theta < \max_{i} x_{i}
\end{cases}
$$
However, we cannot use $\ell'(\theta) = 0$ to find $\hat \theta$ because $\hat \theta$ is on the boundary or at a discontinuous point.
![sta2002_uniform_mle_Ltheta.png\|479](/img/user/%E9%99%84%E4%BB%B6/sta2002_uniform_mle_Ltheta.png)
Hence, we need to introduce indicator function to rewrite $L(\theta)$.
Indicator function is 
$$
\mathbb{1}\{A\} = \begin{cases} 1, & \text{若条件 } A \text{ 成立} \\ 0, & \text{若条件 } A \text{ 不成立}\end{cases}
$$
Rewrite $L(\theta)$,
$$
\begin{align}
f(x;\theta)&= \frac{1}{\theta} \mathbb 1_{\{x\in [0,\theta] \}} \\
L(\theta)&= \prod^n_{i=1}\frac{1}{\theta} \mathbb 1_{\{x\in [0,\theta] \}} \\
&= \frac{1}{\theta^n}\mathbb 1_{\{0\le \min_{i}\{x_{i} \}, \max_{i}\{x_{i} \} \le \theta \}} \\
&= \begin{cases} \theta^{-n}, & \theta \ge \max_i x_i \\ 0, & \text{Otherwises}\end{cases}
\end{align}
$$
The domain of $L(\theta)$ now becomes $\theta \in [\max_i x_{i}, \infty)$. 
Hence, $\hat \theta = \max_i \{x_i \}$, which is the min. point within the domain.

> [!important]
> $\hat \theta = \hat \theta(X_1,\cdots, X_n)$ is MLE of $\theta$ if 
> $$
> \hat \theta = \arg \max L(\theta; X_1, \cdots, X_{n})
> $$
> It means $L(\theta; X_1, \cdots, X_{n})$ achieves its max. value at $\hat \theta$










