---
{"dg-publish":true,"permalink":"/csc-3001-discrete-math/methods-of-proofs/","created":"2026-10-05T18:53:49.279+08:00","updated":"2026-10-27T02:10:15.870+08:00","dg-note-properties":{}}
---


## Direct Proof
Write assume $P$, the show $Q$ is logically follows

**Example:** Prove the sum of 2 even numbers is even
$$
\begin{align}
x &= 2m \\
y &= 2n \\
x+y &= 2m+2n \\
&= 2(m+n)
\end{align}
$$
## Contrapositive
Prove the contrapositive
i.e. Proving "if $P$, then $Q$" is equivalent to proving "if not $Q$, then not $P$"
### Example
- **Claim:** If $r$ is irrational, then $\sqrt{r}$ is irrational.
- **Proof**
	1. If $\sqrt{r}$ is rational, $\sqrt{r}= \frac{a}{b}$ for some integers $a,b$
	2. Hence, $r = \frac{a^2}{b^2}$, $a^2, b^2$ are integers
	3. Hence, $r$ is rational.

> [!tip]
> If $\sqrt{r}$ is rational, then $r$ is rational.
> Hence, if $r$ is irrational, then $\sqrt{r}$ is also irrational.

- **Claim:** For an integer $n$, $n$ is even if and only if $n^2$ is even
{ #6c9076}

- **Proof:** Prove $P\to Q$ and $\neg P \to \neg Q$
	- If $n$ is even, then $n^2$ is even
$$
\begin{aligned}
n &= 2k \\
n^2 &= 4k^2 \\
&= 2(2k^2)
\end{aligned}
$$
	- If $n$ is odd, then $n^2$ is odd
$$
\begin{aligned}
n &= 2k+1\\
n^2 &= (2k+1)^2 \\
&= 4k^2 + 4k + 1 \\
&= 2(2k^2 + 2k) + 1
\end{aligned}
$$

## Proof by Contradiction
Prove $\neg P$ would lead to ridiculous result, so $P$ must be true.
### Example
- **Claim:** $\sqrt{2}$ is irrational
- **Proof**
	1. Suppose $\sqrt{2}$ was rational
	2. Choose integer $m,n$ without common prime factors (代表分数已经约到最简), s.t. $\sqrt{2} = \frac{m}{n}$
$$
\begin{aligned}
\sqrt{2} &= \frac{m}{n} \\
\sqrt{2}n &= m \\
2n^2 &= m^2
\end{aligned}
$$
		Hence, $m$ is even from the proof of example above  [[CSC3001 Discrete Math/Methods of Proofs#^6c9076\|#^6c9076]]
$$
\begin{aligned}
m &= 2l \\
m ^2 &= 4l^2 \\
2n^2 &= 4l^2 \\
n^2 &= 2l^2
\end{aligned}
$$
		Hence, $n$ is also even
	3. If $m$ and $n$ are both even, thus there are a common factor 2, which is contradiction
> [!tip]
> 首先假设 $\sqrt{2}$ 是 rational number，即它可以以 $\frac{a}{b}$ 形式表达，且该分数是约到最简
> 之后用 $\sqrt{2} = \frac{m}{n}$ 进行运算，发现 $m,n$ 都是 even number，则它们都有一个共同的因数 2，与假设相悖，因而证伪

- **Claim:** There are infinitely many prime number
- **Proof**
	1. Assume there are only finitely many primes, denoted by $p_1, p_2, \cdots, p_k$
	2. **Claim:** Any integer $n>1$ is divisible by a prime number
		1. Let $n$ be integer, $n>1$
		2. If $n$ is prime number, then the claim is proved
		3. Otherwise $n = ab$, both $a,b$ are smaller than $n$, $a,b>1$
			1. If $a$ / $b$ is prime number, then the claim is proved
			2. Otherwise, $a=cd$, both $c,d$ are smaller than $a$
				1. If $c$ / $d$ are prime number, then the claim is proved
				2. Otherwise, repeat steps 1-3.
				3. As the no. are getting smaller & smaller, it will eventually stop until a prime factor of $n$ is found
	3. **Lemma:** if $a$ is divided by $p$, then $a+1$ cannot be divided by $p$ for $p>1$
	4. Hence
		1. $a=cp$ for some integer $c$
		2. $a+1 = dp$ for some integer $d$
		3. $1 = (d-c)p$
		4. It is contradiction because $p>=2$ (1 is not prime number)
	5. Hence, by the claim, none of $p_1 \cdots p_k$ can divide $p_1 \cdots p_k + 1$, which is contradiction.

> [!tip]
> 使用 prove by contradiction 证有无数个质数
> 1. 假设质数的数量有限，定义全部质数为 $P = p_1, p_2,\cdots, p_k$ 
> 2. 定义 $N = p_1 p_2 \cdots p_k + 1$
> 3. 当 $N$ 除以全部质数中的每一个质数 $p_i$  时，余数为 1
> 4. 因此存在一个质因数 $p_n$ 可以整除 $N$
> 	1. 所有合成数都是由质因数组成（第二步 proof）
> 5. $p_n$ 并不存在于全部质数 $P$ 之中， 与假设冲突，因此证伪

## Proof by Cases
$$
\begin{aligned}
p &\vee q \\
p &\to r \\
q &\to r \\
\therefore r
\end{aligned}
$$
### Example
- **Claim:** $\forall$ odd $n,\exists m,n^2 = 8 m+1$
- **Proof**
	- Consider $(2 k+1)^2$
	- $(2 k+1)^2 = 4 k^2+ 4 k + 1 = 4(k^2+k)+1$
		- If $k$ is even, then $(k^2 +k)$ is even. The claim is proved
		- If $k$ is odd, then $(k^2 + k)$ is even. The claim is proved

- **Question:** If $a$ and $b$ are irrational, can $a^b$ be rational?
	- 问题是问，如果 $a$ 和 $b$ 是无理数，那 $a^b$ **可不可以**是有理数
		- 「可不可以」把问题变成「有没有可能是」
	- Use $\sqrt{2}$ as example
		- $\sqrt{2}^{\sqrt{2}}$ can either be rational or irrational
			- If it is rational, then it is solved
			- If it is irrational, then $\sqrt{2}^{\sqrt{2}^\sqrt{2}} = \sqrt{2}^{\sqrt{2} \cdot \sqrt{2}} = \sqrt{2}^2 = 2$
				- $\sqrt{2}^{\sqrt{2}^\sqrt{2}}$ is rational number. Hence, it is proved.