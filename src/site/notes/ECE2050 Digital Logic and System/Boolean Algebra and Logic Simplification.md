---
{"dg-publish":true,"permalink":"/ece-2050-digital-logic-and-system/boolean-algebra-and-logic-simplification/","created":"2026-10-28T17:32:30.083+08:00","updated":"2026-11-02T11:11:58.078+08:00","dg-note-properties":{}}
---


## Combinational Circuits
![Logic Circuit.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/Logic%20Circuit.png)
- 输入（inputs）
- 输出（outputs）
- **功能规格（functional specification）：** 输入和输出之间"逻辑上"是什么关系
- **时序规格（timing specification）：** 输出相对于输入"什么时候"才有效
![Combinational Circuits.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/Combinational%20Circuits.png)
- Node
	- **Inputs:** A,B,C
	- **Outputs:** Y,Z
	- **Internal:** n1
- Circuit elements: E1, E2, E3

- Combinational logic: Memoryless
	- Outputs determined by current values of output
- Sequential logic
	- Outputs determined by previous & current values of inputs

A circuit is combinational circuits if
- Every element is combinational
- Every node is either an input / connect to exactly one output
- The circuit contains no cyclic paths 没有环状路径
## Boolean Algebra - Axioms & Theorems
*Skip*
## SOP, POS
- **Literal:** A variable / its complement
	- e.g. $A,\overline A, B, \overline B$
- **Implicant:** Product of literals
	- e.g. $AB, AB\overline C$
- **Minterm:** Product that includes all input variables
	- e.g. $AB\overline C$
- **Maxterm:** Sum that includes all input variables
	- e.g. $A+B+\overline C$

### Sum-of-Products (SOP)
- All boolean equations can be written in SOP form
- All products contain literals only

| 判定       | 表达式                | 说明                |
| -------- | ------------------ | ----------------- |
| ✅ SOP    | $Y = AB + BC + DE$ | 三项，每项都是纯乘积        |
| ❌ 不是 SOP | $Y = DF + E(A+B)$  | E(A+B) 里和了加法      |
| ✅ SOP    | $Z = A + BC + DEF$ | A 是"只有一个文字的乘积"，允许 |

- Each row has a minterm
- Adding up of all minterms with output 1 can get the function
	- reason why it called **Sum of Product**

| A   | B   | Y     | Minterm        | Minterm name |
| --- | --- | ----- | -------------- | ------------ |
| 0   | 0   | 0     | $\bar A\bar B$ | $m_0$        |
| 0   | 1   | **1** | $\bar AB$      | $m_1$        |
| 1   | 0   | 0     | $A\bar B$      | $m_2$        |
| 1   | 1   | **1** | $AB$           | $m_3$        |
By adding up all minterms with output 1, we get
$$
Y = F(A,B) = \overline A B + AB
$$
- **Standard SOP Form:** All the variables in the domain appear in each product term

### Product-of-Sums (POS) Form
- All boolean equations can be written in SOP form
- All sums contains literals only

|判定|表达式|说明|
|---|---|---|
|✅ POS|Y = (A+B)(C+D)(E+F)|三项，每项都是纯和|
|❌ 不是 POS|Y = (D+E)(F+GH)|(F+GH) 里乘了乘法|
|✅ POS|Z = A(B+C)(D+E)|A 是"只有一个文字的和"，允许|

- Each row has a maxterm
- Each maxterm is FALSE for that row and only for that row
- By multiplying all the maxterms with output 0 can get the function
	- reason why it called **Product of Sums**

| A   | B   | Y     | Maxterm           | Maxterm name |
| --- | --- | ----- | ----------------- | ------------ |
| 0   | 0   | **0** | $A + B$           | $M_0$        |
| 0   | 1   | 1     | $A + \bar B$      | $M_1$        |
| 1   | 0   | **0** | $\bar A + B$      | $M_2$        |
| 1   | 1   | 1     | $\bar A + \bar B$ | $M_3$        |
By multiplying all maxterms with output 0, we get
$$
Y = F(A,B) = (A+B) \cdot (\overline A + B)
$$
- **Standard POS Form:** All the variables in the domain appear in each sum term

**Prove SOP = POS**
**Goal:** Prove $\overline A B + AB \equiv (A+B) \cdot (\overline A + B)$
$$
\begin{aligned}
R.H.S. &= (A+B) \cdot (\overline A + B) \\
&= A\overline A + AB + B\overline A  + BB \\
&= 0 + AB + \overline A B + B \\
&= B(A+\overline A) + B \\
&= B+B \\
&= B \\
L.H.S. &= \overline A B + AB \\
&= B(\overline A + A) \\
&= B \\
&= R.H.S.
\end{aligned}
$$
Hence, POS and SOP are equivalent.
