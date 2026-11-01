---
{"dg-publish":true,"permalink":"/ece-2050-digital-logic-and-system/combinational-logic-design/","created":"2026-10-28T21:22:44.910+08:00","updated":"2026-11-01T12:51:00.457+08:00","dg-note-properties":{}}
---


## Basic Combinational Logic Circuits
### AND-OR Logic
**Two-level logic:** ANDs followed by ORs
- e.g. $Y = \bar A \bar B \bar C + A \bar B \bar C + A \bar B C$
Implement functions in SOP form
### AND-OR-Invert Logic
**Two-level logic:** ORs followed by ANDs
- e.g. $Y = \overline{AB + CD} = (\bar A + \bar B)(\bar C + \bar D)$
Implement function in POS form
![AND-OR-Invert Logic.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/AND-OR-Invert%20Logic.png)
### Exclusive OR (XOR) Logic
$$
X = A \bar B + \bar A B = A \oplus B
$$
![XOR Logic.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/XOR%20Logic.png)
### Exclusive-NOR (NXOR) Logic
$$
\begin{aligned}
X &= \overline{A \bar B + \bar A B} \\
&= \overline{(A \bar B)}\ \overline{(\bar A B)} \\
&= (\bar A + B)(A + \bar B) \\
&= \bar A \bar B + A B
\end{aligned}
$$
![NXOR Logic.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/NXOR%20Logic.png)

## NAND, NOR: Universal Property
**通用门（universal gate）：** 只用这一种门就能实现 NOT、AND、OR 等一切逻辑功能
### The Universal Property of NAND Gates
Combination of NAND gates can function as NOT, AND, OR and NOR
- 1 NAND gate $\to$ Inverter
- 2 NAND gate $\to$ AND gate
- 3 NAND gate $\to$ OR gate
- 4 NAND gate $\to$ NOR gate
![The Universal Property of NAND Gates.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/The%20Universal%20Property%20of%20NAND%20Gates.png)

### The Universal Property of NOR Gates
Combination of NOR gates can function as NOT, AND, OR and NAND
- 1 NOR gate $\to$ Inverter
- 2 NOR gate $\to$ OR gate
- 3 NOR gate $\to$ AND gate
- 4 NOR gate $\to$ NAND gate
![The Universal Property of NOR Gates.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/The%20Universal%20Property%20of%20NOR%20Gates.png)
## Bubble Pushing
- Backward
	- Add bubbles to inputs
- Forward
	- Add bubble to output
![De Morgan’s Theorem - Gates.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/De%20Morgan%E2%80%99s%20Theorem%20-%20Gates.png)
### Bubble Pushing Rules
1. **Begin at output, then work toward inputs** —— 从输出端开始，朝输入端方向推进；
2. **Push bubbles on final output back** —— 把**最终输出上的气泡往后推**（推到电路的内部去）；
3. **Draw gates in a form so bubbles cancel** —— 把每个门画成 "气泡能抵消" 的形式。
