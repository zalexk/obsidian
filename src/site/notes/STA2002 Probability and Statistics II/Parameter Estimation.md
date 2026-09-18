---
{"dg-publish":true,"permalink":"/sta-2002-probability-and-statistics-ii/parameter-estimation/","created":"2026-09-15T00:18:08.693+08:00","updated":"2026-09-18T11:03:00.105+08:00","dg-note-properties":{}}
---


## Data Visualization
Histogram is used to visualize continuous observations by grouping data into several bins
- **Height:** Relative frequency / density of data points
	- **Relative frequency:** $\frac{\text{\# of data in the bin}}{\text{\# of total data}}$
	- **Density:** $\frac{\text{Relative frequency}}{\text{Bin width}}$
	- Let there are $k$ bins,  the bin width of $j$ be $w_j$, and the number of data observed in the bin is $n_j$.
		- Relative frequency = $\frac{n_j}{n}$
		- Density = $\frac{n_j}{w_j n}$
			- Always equal to 1 for all bins: $\sum_{j=1}^k w_j \left(\frac{n_j}{w_j n} \right)= 1$
	- ![histogram.png](/img/user/%E9%99%84%E4%BB%B6/histogram.png)
- **Area:** Proportional to the num. of observations 
In PDF, probability is the area under the density curve. 
Histogram is the discrete version for PDF.

The bin size (num. of bins) is important
- **Tow small:** Overfit
- **Too large:** Hide important details & patterns in the data
### Boxplot

$$
\min, \overbrace{\underbrace{Q_1}_\frac{1}{4}, \underbrace{Q_2}_{\text{median}}, \underbrace{Q_3}_\frac{3}{4}}^{\text{Interquartile range}}, \max
$$
![boxplot.png](/img/user/%E9%99%84%E4%BB%B6/boxplot.png)
- IQR = $Q_3-Q_ 1$
- Fence
	- **Inner fence:** Left /right of box at distance $(1.5\times IRQ)$
	- **Outer fence:** Left / right of box at distance $(3\times IRQ)$
- Whisker
	- **Lower whisker:** From $Q_1 - 1.5 \ IQR$ to $\min$ 
	- **Upper whisker:** From $\max$ to $Q_3 +1.5 \ IQR$
- **Suspect outlier:** Between inner & outer fence $(3 \times IQR > x > 1.5 \times IQR)$ or $(-1.5 \times IQR< x < -3\times IQR )$
- **Outlier:** Beyond the outer fence ($x>3 \times IRQ$ or $x<-3\times IQR$ )
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
- Data are normally distributed
### Parameter Space
Suppose sample $X_1, \cdots, X_2$ are random and i.i.d. with unknown parameter $\theta$ and PMF / PDF $f(x;\theta)$.
The parameter $\theta$ tasks value in the parameter space $\Omega$ (i.e. domain of $\theta$)
> [!note]
> 在之后求解 MLE 时起到硬约束的作用（不可以取超过 $\Omega$ 的值）


> **Example**
> For the PDF of normal distribution,
> $$
f(x) = \frac{1}{\sigma \sqrt{2\pi}} \exp \left[ -\frac{(x-\mu)^2}{2\sigma^2}\right], \quad -\theta < x < \theta
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
\underbrace{u(x_1,\ldots,x_n)}_{\text{Point estimator：Single value}}
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
$$
\begin{align}
f(x_{};p) &= p^x (1-p)^{1-x}, \quad x\in\{0,1\}, \quad 0\le p \le 1\\ 
L(p) &= \prod_{{i=1}}^n p^{x_{i}} (1-p)^{1-x_{i}} \\
&= p^{\sum_{i=1}^n x_{i}} (1-p)^{\sum_{i=1}^n 1-x_{i}} \\
\ell (p) &=   
\end{align}
$$