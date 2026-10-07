---
{"dg-publish":true,"permalink":"/csc-3001-discrete-math/first-order-logic/","created":"2026-10-04T11:20:46.455+08:00","updated":"2026-10-06T12:49:31.664+08:00","dg-note-properties":{}}
---

## Quantifiers
> [!important] 
> Predicates are propositions with variables

e.g. $P(x,y) = x+2=y$

When there is a variable, we need to specify the domain
> [!important]
> Domain of a variable is the set of all values that may be substituted in place of the variable

### Universal and Existential Quantifier
The truth of quantified statement depends on the domain
- **Universal quantifier:** $\forall x\in A$ means **for all** $x$ in $A$
	- $\forall x \in \mathbb Z^+, P(x):P(1)\wedge P(2)\wedge \cdots$
- **Existential quantifier:** $\exists x\in A$ means **there exists** some $x$ in $A$
	- $\exists x\in \mathbb Z^+, P(x): P(1)\vee P(2)\vee \cdots$
### Translating Mathematical Theorem
> If an integer $n$ is greater than 2, then the equation $a^n + b^n = c^n$ has no solution in positive integers $a,b,c$

1. Find domain: $\forall a,b,c \in \mathbb Z^+, (n\in \mathbb Z)\wedge (n>2)$
2. Find condition: $a^n + b^n \ne c^n$
3. Convert to $p\to q$ format: $\forall a,b,c \in \mathbb Z^+. (n\in \mathbb Z)\wedge (n>2) \to a^n + b^n \ne c^n$
4. Simplify: $\forall a,b,c\in \mathbb Z^+. (n\le 2)\vee (n\notin \mathbb Z)\vee (a^n + b^n \ne c^n)$

> Every positive even number at least 6 is a sum of two primes
> Suppose given predicates $\text{prime}(x), \text{even}(x)$
1. Find domain: $\forall n \in \mathbb{Z}^{+}.\ \big[\text{even}(n) \wedge (n \ge 6)\big]$
2. Find condition: $\exists p,q \in \mathbb{Z}.\ \text{prime}(p) \wedge \text{prime}(q) \wedge (p+q = n)$
3. Convert to $p\to q$ format: $\forall n \in \mathbb{Z}^{+}.\ \big[\text{even}(n) \wedge (n \ge 6)\big] \to \big[\exists p,q \in \mathbb{Z}.\ \text{prime}(p) \wedge \text{prime}(q) \wedge (p+q = n)\big]$
4. Simplify: $\forall n \in \mathbb{Z}^{+}.\ \text{odd}(n) \vee (n < 6) \vee \big[\exists p,q \in \mathbb{Z}.\ \text{prime}(p) \wedge \text{prime}(q) \wedge (p+q=n)\big]$
$$
\begin{aligned}  
&\forall n \in \mathbb{Z}^{+}.\ \big[\text{even}(n) \wedge (n \ge 6)\big] \to \big[\exists p,q \in \mathbb{Z}.\ \text{prime}(p) \wedge \text{prime}(q) \wedge (p+q = n)\big] \\[4pt]  
\quad \equiv\ &\forall n \in \mathbb{Z}^{+}.\ \neg\big[\text{even}(n) \wedge (n \ge 6)\big] \vee \big[\exists p,q \in \mathbb{Z}.\ \cdots \big] \\[4pt]  
\quad \equiv\ &\forall n \in \mathbb{Z}^{+}.\ \big[\text{odd}(n) \vee (n < 6)\big] \vee \big[\exists p,q \in \mathbb{Z}.\ \text{prime}(p) \wedge \text{prime}(q) \wedge (p+q = n)\big] \\[4pt]  
\quad \equiv\ &\forall n \in \mathbb{Z}^{+}.\ \text{odd}(n) \vee (n < 6) \vee \big[\exists p,q \in \mathbb{Z}.\ \text{prime}(p) \wedge \text{prime}(q) \wedge (p+q = n)\big]  
\end{aligned}
$$
## Negation
$$
\neg \forall xP(x) \equiv \exists x\neg P(x)
$$
e.g. Not everyone likes football = There exists someone who doesn’t like football.
> [!note] Proof
> Assume the domain is $\{1,2,3\}$
> $$
> \begin{align}
> \neg \forall xP(x) &= \neg(P(1)\wedge P(2)\wedge P(3)) \\
> &= \neg P(1) \vee \neg P(2) \vee \neg P(3) \\
> &= \exists x \neg P(x) \\
> &= R.H.S.
> \end{align}
> $$

$$
\neg \exists x P(x) \equiv \forall x\neg P(x)
$$
e.g. Not exists a plant that can fly = every plant cannot fly
## Multiple Quantifiers
### Order of Quantifiers
| 维度       | **命题 A** (普遍量化优先)                                                      | **命题 B** (存在量化优先)                                                       |
| -------- | ---------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| **自然语言** | “防病毒软件杀所有计算机病毒” <br>(Each virus has a killer)                          | “存在一个杀软能干掉所有病毒” <br>(One killer kills everything)                       |
| **逻辑公式** | $$ \forall v \cdot \exists a \cdot \text{kills}(a,v) $$                | $$ \exists a \cdot \forall v \cdot \text{kills}(a,v) $$                 |
| **约束范围** | **弱约束**。  <br>($\exists$ 在外层受 $\forall$ 支配)  <br>只要对当前 $v$ 能找到 $a$ 就行。 | **强约束**。  <br>($\forall$ 在内层被 $\exists$ 锁死)  <br>选定后的 $a$ 必须对所有 $v$ 有效。 |
Hence, order of quantifiers is important.

## Arguments of Quantified Statements
### Predicate Calculus Validity
- **Propositional logic:** A technology is no matter what the truth value of $A$ and $B$ are.
	- 对 $A,B$ 的所有真假组合都为真
- **First-order logic:** A tautology is no matter what the domain of $x,y,z$ or $P, Q$ are
	- 对任意论域 domain + 任意谓词含义 predicate 都为真

> [!important]  
> A quantified argument is valid if the conclusion is true whenever the assumptions are true

### Arguments with Quantified Statements
- Universal instantiation
$$
\begin{align}
\forall x, P(x) \\
\therefore P(a)
\end{align}
$$
如果所有 $x$ 都满足 $P$，那么随便挑一个具体的 $a$，它当然也满足 $P$。
- Universal modus ponens
$$
\begin{align}
\forall x, P(x) \to Q(x) \\
P(a) \\
\therefore Q(a)
\end{align}
$$
如果所有 $x：P(x) \Rightarrow Q(x)$，而某个 $a$ 满足 $P$，那么 $a$ 一定满足 $Q$。
- Universal modus tollens
$$
\begin{align}
\forall x, P(x) \to Q(x) \\
\neg Q(a) \\
\neg P(a)
\end{align}
$$
如果所有 $x：P(x) \Rightarrow Q(x)$，而某个 $a$ 不满足 $Q$，那么 $a$ 一定不满足 $P$。

### Universal Generalization
When $c$ is independent of $A$,
$$
\begin{align}
A \to R(c) \\
\therefore A\to \forall x. R(x)
\end{align}
$$
If $R(c)$ is true for an arbitrary $c$, then the statement is true for all values.
