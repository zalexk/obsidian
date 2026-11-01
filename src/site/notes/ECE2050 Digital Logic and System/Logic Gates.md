---
{"dg-publish":true,"permalink":"/ece-2050-digital-logic-and-system/logic-gates/","created":"2026-10-13T15:01:40.977+08:00","updated":"2026-11-01T12:50:49.863+08:00","dg-note-properties":{}}
---


## Logic Gates
- Perform logic function
	- Inversion (NOT)
	- AND
	- OR
	- NAND
	- NOR
- Single input
	- NOT gate
	- Buffer
- Two-input / Multiple-input
	- AND
	- OR
	- XOR
	- NAND
	- NOR
	- XNOR
### The Inverter
![inverter.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/inverter.png)
$$
X = \overline A
$$
### Single-Input Gate
![Single-Input Gate.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/Single-Input%20Gate.png)
### The AND Gate
![AND Gate.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/AND%20Gate.png)
$$
X = AB
$$
### The OR Gate
![OR Gate.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/OR%20Gate.png)
$$
X = A+B
$$
### The NAND Gate
![NAND Gate.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/NAND%20Gate.png)
$$
X = \overline{AB} = \overline A + \overline B
$$
> [!note]
> NAND $\equiv$ NOR

### The NOR Gate
![NOR Gate.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/NOR%20Gate.png)
$$
X = \overline{A+B} = \overline A \ \overline B
$$
### The Exclusive-OR (XOR) Gate
![XOR Gate.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/XOR%20Gate.png)
$$
X = A \oplus B
$$
> [!tip]
> $A$ 和 $B$ 值不一致为 TRUE

可以用作两 bits 相加
![XOR - Application.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/XOR%20-%20Application.png)
### The Exclusive-NOR (XNOR) Gate
![XNOR Gate.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/XNOR%20Gate.png)
$$
X = \overline{A\oplus B}
$$
> [!tip]
> $A$ 和 $B$ 值一致为 TRUE

### Multiple-Input Logic Gate
![NOR3 + AND3.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/NOR3%20+%20AND3.png)

For multi-input XOR, it will output TRUE if an odd number of inputs are TRUE
Hence, it can used to perform odd parity

![ECE2050-Chap3-fig01-gate-symbols.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/ECE2050-Chap3-fig01-gate-symbols.png)
#### Example
> This is a cold storage alarm system. 
> Normally, a door-open timeout or high temperature trigger an automatic alarm. 
> Maintenance mode disables auto alarms, but the test button still triggers them.
> $D=1$: door open too long;
> $H=1$: temperature too high;
> $M=1$: maintenance mode;
> $Tn=0$: test button pressed
1. Write the Boolean expression for Y
$$
\begin{aligned}
Y &= \overline M(D + H) + \overline{Tn}
\end{aligned}
$$

2. Draw the circuit using only NOT, 2- input AND, and 2-input OR gates
![Logic Gate - Example 1.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/Logic%20Gate%20-%20Example%201.png)
## Logic Levels
Discrete voltages represent $1$ and $0$
- Ground (GND) = 0
- $V_{DD}$ = 1
Noise is anything that degrades the signals, e.g. resistance
- e.g. A gate outputs 5 V but the receiver gets 4.5 V due to resistance
### Noise Margins
- High noise margin: $NM_H = V_{OH} - V_{IH}$
- Low noise margin: $NM_L =V_{IL} - V_{OL}$

> [!tip]
> - $NM$ = Noise Margin
> - $OH$ = Output High
> - $IH$ = Input High
> - $IL$ = Input Low
> - $OL$ = Output Low

|**符号**|**含义**|**性质**|
|---|---|---|
|$V_{OH}$|输出高电平的**最低值**|驱动端承诺：我输出 1 时不会低于它|
|$V_{OL}$|输出低电平的**最高值**|驱动端承诺：我输出 0 时不会高于它|
|$V_{IH}$|被判为 1 的**最低**输入电压|接收端承诺：高于它就认 1|
|$V_{IL}$|被判为 0 的**最高**输入电压|接收端承诺：低于它就认 0|
![Noise Margin.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/Noise%20Margin.png)
#### DC Transfer Characteristics
$V_{IL}$ 和 $V_{IH}$ 是根据的电压传输特性（VTC）取的值，是曲线中 slope = 1 的值

在 real buffer, $NM_H, NM_{L} < \frac{V_{DD}}{2}$ 
![DC Transfer Characteristics.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/DC%20Transfer%20Characteristics.png)

### VDD Scaling
$V_{DD}$ has dropped to
- Avoid frying tiny transistors 避免烧坏越做越小的晶体管
- Save power 省电
#### Example
> Sensor: $V_{OL}=0.40 V$, $V_{OH}=1.40 V$. 
> Input gate: $V_{IL}=0.80 V$, $V_{IH}=2.10 V$
> Classify measured inputs 0.35 V, 1.42 V, and 2.55 V, Which one may be received incorrectly without buffer?
$$
\begin{aligned}
0.35V &< 0.80V \to 0 \\
0.80V < 1.42V &< 2.10V \to \text{ unknown } \\
2.55V &> 2.10V \to 1
\end{aligned}
$$
