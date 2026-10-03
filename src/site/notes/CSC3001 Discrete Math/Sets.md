---
{"dg-publish":true,"permalink":"/csc-3001-discrete-math/sets/","created":"2026-09-14T22:11:36.124+08:00","updated":"2026-10-04T02:09:14.967+08:00","dg-note-properties":{}}
---

## Basic Definition
> [!important] Definition
> A set is an **unordered** collection of **distinct** objects.
> - 无序
> - 唯一

The objects in a set are called the elements / members of the set.
$$
\begin{align}
A &= \{ 2,3,4,5\} \\
&= \{5,3,2,4\}
\end{align}
$$
- $S = \{2,3,5,3,7\}$ is not a set due to duplicated objects $3$
- $S = \{ \{a\}, a\}$ is a set because the objects in the set are unordered and distinct

> [!Important] Definition
> Power set is set of all subsets of $A$
> Let $A= \{x,y\}$
> -  $\text{pow}(A) = \{\emptyset, \{x\}, \{y\} , \{x,y\} \}$
> - $|\text{pow}(A)| = 2^{|A|}$

### Defining Sets by Properties
**背景：** 有时候只靠列出所有 elements 来定义一个 sets 是不可能的，因此我们可以用公式来定义 sets，只要 element 符合公式，则为 set 的元素

Define the set by $\{ x\in A | P(x)\}$.

e.g. $S = \{ x\in \mathbb R | -2< x<5\}$ means $S$ is a real number which is in $(-2,5)$.
e.g. $S=\{x\in \mathbb Z|x\ge 0\}$ means $S$ is non-negative integer

> [!important] Definition
> $|S|$ is the size of $S$
> e.g. $|\emptyset| = 0$

### Membership
> [!important] Definition
> - $x\in A$: $x$ is an element of $A$
> - $x \notin A$: $x$ is not an element of $A$
> - $A\subseteq B$: $A$ is a subset of $B$
> 	- For any $x\in A$, we have $x\in B$
> 	- **通俗来说：** $A$ 在 $B$ 里面，$A$ 可能等于 $B$
> - $A = B$: $A \subseteq B$ and $B \subseteq A$
> - $A\subset B$: $A$ is proper subset of $B$
> 	- $A\subseteq B$ and $A\ne B$
> 	- **通俗来说：** $A$ 在 $B$ 里面，但是 $A$  不等于 $B$

---
## Operations on Sets
- Intersection
$$
A\cap B = \{ x \in \underbrace{\mathbb U}_{\text{Universe}}| x\in A\text{ and } x\in B\}
$$
	- Two sets are disjoint if $A\cap B = \emptyset$ 
- Union
$$
A\cup B= \{ x \in \mathbb U | x \in A \text{ or } x \in B\}
$$
	- $|A\cup B| = |A|+|B|-|A\cap B|$
- Complement
$$
\bar A = A^c = \{ x\in \mathbb U| x\notin A\}
$$
	- If $A\subseteq B$, then $\bar B \subseteq \bar A$
- Difference
$$
A-B = \{x\in \mathbb U | x\in A \text{ and }x\notin B \}
$$
	- $|A-B| = |A| - |A\cap B|$
![Basic Operations on Sets.png](/img/user/%E9%99%84%E4%BB%B6/Basic%20Operations%20on%20Sets.png)
### Indexed Collection of Sets
> [!tip]
> Indexed collection of sets 跟上文的 intersection 和 union 无异。
> 区别在于其支持批量运算，可以求一大堆 sets 的 intersection 和 union。

$$
\begin{align}
\bigcup_{i=0}^{n} A_i &= \{x \in U \mid x \in A_i \text{ for at least one } i = 0, 1, 2, \dots, n\} \\
\bigcup_{i=0}^{\infty} A_i &= \{x \in U \mid x \in A_i \text{ for at least one nonnegative integer } i\} \\
 \\
\bigcap_{i=0}^{n} A_i &= \{x \in U \mid x \in A_i \text{ for all } i = 0, 1, 2, \dots, n\} \\
\bigcap_{i=0}^{\infty} A_i &= \{x \in U \mid x \in A_i \text{ for all nonnegative integers } i\}
\end{align}
$$
> [!tip]
> - Union 是至少任一一个 set 里面有
> - Intersection 是每一个 set 里面都有

#### Example
> For each positive integer $i$, let $A_i = \left\{ x\in \mathbb R | -\frac{1}{i} < x < \frac{1}{i}  \right\}$
> Equivalently, $A_i = \left( -\frac{1}{i}, \frac{1}{i} \right)$
> a. Find $A_1 \cup A_2 \cup A_3$ and $A_1 \cap A_2 \cap A_3$
> b. Find $\bigcup^\infty_{i=1} A_i$ and $\bigcap^\infty_{i=1} A_i$

$$
\begin{align}
A_1 \cup A_2 \cup A_3 &= (-1,1)\cup \left( -\frac{1}{2}, \frac{1}{2} \right)\cup \left( -\frac{1}{3}, \frac{1}{3} \right) \\
&= (-1, 1) \\
A_1 \cap A_2 \cap A_3 &= (-1,1)\cap \left( -\frac{1}{2}, \frac{1}{2} \right)\cap \left( -\frac{1}{3}, \frac{1}{3} \right) \\
&= \left( -\frac{1}{3}, \frac{1}{3} \right) \\
 \\
\bigcup^\infty_{i=1} A_i &= (-1,1)\cup \left( -\frac{1}{2}, \frac{1}{2} \right)\cup \left( -\frac{1}{3}, \frac{1}{3} \right) \cup \cdots \\
&= (-1,1) \\
\bigcap^\infty_{i=1} A_i &= (-1,1)\cap \left( -\frac{1}{2}, \frac{1}{2} \right)\cap \left( -\frac{1}{3}, \frac{1}{3} \right) \cap \cdots \\
&= \{0\}
\end{align}
$$
### Partitions of Sets
> [!important] Definition
> A collection of non-empty sets $\{A_1, \cdots, A_n\}$ is a partition of a set $A \iff$
> - $A = A_1 \cup A_2\cup \cdots \cup A_n$
> - $A_1, A_2, \cdots , A_n$ are mutually disjoint / pairwise disjoint

![partitions of sets.png](/img/user/%E9%99%84%E4%BB%B6/partitions%20of%20sets.png)
### Cartesian Products
> [!Important] Definition
> Given 2 sets $A$ and $B$, the Cartesian product $A\times B$ is the set of all ordered pairs $(a,b)$, where $a\in A, b\in B$
> $$
> A\times B = \{(a,b) | a\in A, b\in B\}
> $$
> It can be generalized to any number of sets
> $$
> A\times B\times C = \{(a,b,c) | a\in A, b\in B, c\in C \}
> $$

> [!tip]
> For ordered pairs, the ordering is important, i.e. $(1,2) \ne (2,1)$

> [!important]
> - If $|A| = n$ and $|B| = m$, 
> 	- then $|A\times B| = nm$
> 	- If $|C| = l$, then $|A\times B\times C| = nml$
> - $|A_1 \times A_2 \times \cdots \times A_k| = |A_1| \times |A_2| \times \cdots \times |A_k|$
> - $\emptyset \times A = \emptyset$
> 	- $|\emptyset \times A |= 0$

### Example
$$
\begin{align}
\text{Let }A &= \{a,b\}, B = \{0,1\} \\
A\times A &= \{(a,a), (a,b), (b,a), (b,b)\} \\
A\times B &= \{(a,0), (a,1), (b,0), (b,1)\} \\
B\times B &= \{(0,0),(0,1),(1,0),(1,1) \}
\end{align}
$$
---
## Set Identities
- Distributive Law 
	- $A \cup (B \cap C) = (A \cup B) \cap (A \cup C)$  
	- $A \cap (B \cup C) = (A \cap B) \cup (A \cap C)$  
- Associative Law  
	- $A \cup (B \cup C) = (A \cup B) \cup C$  
	- $A \cap (B \cap C) = (A \cap B) \cap C$  
- De Morgan's Law  
	- $\overline{(A \cup B)} = \overline{A} \cap \overline{B}$  
	- $\overline{(A \cap B)} = \overline{A} \cup \overline{B}$  
- Complement Law  
	- $A \cup \overline{A} = U$  
	- $A \cap \overline{A} = \emptyset$  
- Commutative Law  
	- $A \cup B = B \cup A$  
	- $A \cap B = B \cap A$  
- Identity Law  
	- $A \cup \emptyset = A$  
	- $A \cap U = A$
- Set Difference Law
	- $A-B = A\cap \overline B$
#### Example
1. Prove $A-(A\cap B) = A-B$
$$
\begin{align}
L.H.S. &= A-(A\cap B) \\
&= A\cap\overline{A\cap B} \quad &\text{Set Difference Law} \\
&= A\cap (\overline A \cup \overline B) &\text{De Morgan's Law} \\
&= (A\cap \overline A) \cup (A\cap \overline B) &\text{Distributive Law}\\
&= \emptyset \cup (A\cap \overline B) \\
&= A\cap \overline B &\text{Identity Law} \\
&= A-B &\text{Set Difference Law} \\
&= R.H.S.
\end{align}
$$
2. Prove $(A\cup B) - C = (A-C) \cup (B-C)$
$$
\begin{align}
L.H.S. &= (A\cup B) - C \\
&= (A\cup B)\cap \overline C \\
&= (A\cap \overline C) \cup (B\cap \overline C) \\
&= (A-C) \cup (B-C) \\
&= R.H.S.
\end{align}
$$
3. Prove $\overline{(A\cup B \cup C)} = \overline A \cap \overline B\cap \overline C$
$$
\begin{align}
L.H.S. &= \overline{(A\cup B \cup C)} \\
&= \overline{(A\cup B)} \cap \overline C \\
&= \overline A \cap \overline B \cap \overline C \\
&= R.H.S.
\end{align}
$$
---
## Russell's Paradox 罗素悖论
> [!caution]
> 以下内容由 AI 基于 Lecture Note 撰写，作者仅进行小幅度的修改。


$$
W := \{S \in \text{Sets} \mid S \notin S\}
$$

即 “$W$ 是所有"不包含自己"的集合的集合”。
现在问: ** $W$ 在不在 $W$ 里?**
- 假设 $W \in W$ ：那么 $W$ 就属于 $W$，而 $W$ 是"不包含自己的集合的集合"，所以 $W$ 应该不包含自己，矛盾。
- 假设 $W \notin W$ ：那么 $W$ 不属于 $W$，说明 $W$ 是"不包含自己的集合"，按 $W$ 的定义，这种集合就应该属于 $W$，矛盾。
两条假设都推出矛盾——这就是著名的**罗素悖论**。它告诉我们: **"任意性质都能定义出一个集合"是错的**。比如"所有集合的集合"、"所有不包含自己的集合"这种"过于庞大"的定义,会落入自指的陷阱。
### 用"理发师悖论"帮助理解
> 一个理发师声称：“我给所有**不自己剃头**的人剃头,但我**不**给那些**自己剃头**的人剃头。”
> 问：理发师给不给自己剃头？
> 如果他给自己剃头，那按规矩他就不该给自己剃头——矛盾。
> 如果他不给自己剃头，那按规矩他就应该给自己剃头——矛盾。

只需记住：**不能把"任意满足性质的全体"都默认成集合**。
### 一点延伸：与停机问题的关系
罗素悖论和 [[CSC3001 Discrete Math/Propositional Logic\|Propositional Logic]] 中所提到的**停机问题 (Halting Problem)** 在推理结构上非常相似。
