---
{"dg-publish":true,"permalink":"/ece-2050-digital-logic-and-system/combinational-building-blocks/","created":"2026-10-29T20:27:35.598+08:00","updated":"2026-11-01T12:50:43.403+08:00","dg-note-properties":{}}
---


## Adders
### Half Adders
$$
\underbrace{\text{2 binary digits}}_{\text{Input}} \Rightarrow \underbrace{\text{2 binary digits: 1 sum bit $\sum$ \& 1 carry bit $C_\text{out}$}}_{\text{Output}}
$$
![Half adders.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/Half%20adders.png)
$$
\begin{aligned}
\sum &= A\oplus B = A\overline B + \overline A B \\
C_{\text{out}} &= AB
\end{aligned}
$$
### Full Adders
$$
\underbrace{\text{2 binary digits + 1 input carry $C_\text{in}$}}_{\text{Input}} \Rightarrow \underbrace{\text{2 binary digits: 1 sum bit $\sum$ \& 1 carry bit $C_{\text{out}}$}}_{\text{Output}}
$$
![Full adders.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/Full%20adders.png)
$$
\begin{aligned}
\sum &= (A\oplus B)\oplus C_{\text{in}} \\
C_{\text{out}} &= AB+(A\oplus B)C_{\text{in}}
\end{aligned}
$$
#### Implemented with Half-adders
![Implemented with Half-adders.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/Implemented%20with%20Half-adders.png)
### Parallel Binary Adders
Formed by 2 or more full-adders
![Parallel Binary Adders.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/Parallel%20Binary%20Adders.png)
#### Parallel Adders: 74HC283 / 74LS283
- 4-bit parallel adders
- Cascade 级联 2 4-bit parallel adders to handle the addition of 2 8-bit number
- For low-order adder,
	- $C_{\text{in}}$ is connected to ground
	- $C_\text{out}$ is connected to $C_\text{in}$ of the high-order adder

> [!tip]
> 低阶 / 高阶”（low-order / high-order）指的就是位权（bit weight）小/大，即该位在二进制数中代表 $2^0$ 还是 $2^7$ （举例）

### The Ripple Carry Adder
Carry output of each full-adder is connected to the carry input of the next higher-order stage (a stage is 1 full-adder)
Hence, the sum & output carry of any stage have to wait for the occurrence of input carry $\to$ time delay in addition process
任何一级的和与进位输出，**都要等到该级的进位输入到位之后**才能产生--这就在加法过程里引入了时间延迟

The input carry to the least significant stage has to ripple through all the adders before a final sum is produced
最低位那一级收到的进位，必须 ripple（涟漪般逐级穿过）所有加法器，最终的和才能出来
### The Look-Ahead Carry Adder
Speed up by eliminating the ripple carry delay
- **Carry generation:** $C_g = AB$
- **Carry propagation:** $C_p = A+B$ (if input carry is 1)
Thus, output carry $C_\text{out} = C_{g} + C_{p}C_{\text{in}}$
![Pasted image 20261030140816.png](/img/user/Pasted%20image%2020261030140816.png)

| $A,B,C_{in}$ | 谁在起作用 | 下面写的字                  | 说明                                                                |
| ------------ | ----- | ---------------------- | ----------------------------------------------------------------- |
| **1 1** 0    | 自己造   | Generated carry        | 两个输入都是 1，**自己冒出**进位；注意图里**没有斜箭头**--因为它压根没用到进来的进位（$C_{in}=0$），实力单干 |
| **1 1** 1    | 两者都成立 | Propagated / Generated | 既自己造、又能把进来的传下去，两种身份重叠，所以箭头画了一堆                                    |
| **1 0** 1    | 只能放行  | Propagated carry       | 自己不造（$C_g=0$），全靠把进来的 1 **透传**下去                                   |
| **0 1** 1    | 只能放行  | Propagated carry       | 同上，这回是 B 在放行                                                      |

**Combine Look-Ahead and Ripple Carry Adders:** Connect the $C_{\text{out}}$ of one adder to the $C_\text{in}$ of the next adder $\to$ cascade 2 look-ahead carry adders
## Comparators
### Equity
XNOR gate can be used as basic comparators 比较器
![Comparators - Equality.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/Comparators%20-%20Equality.png)
The equality comparison of 2 2-bit numbers
![equality comparison of 2 2-bit numbers.png](/img/user/ECE2050%20Digital%20Logic%20and%20System/Attachment/equality%20comparison%20of%202%202-bit%20numbers.png)
### Inequality
The output are
- $A>B$
- $A=B$
- $A<B$
Procedures
1. Check from highest-order bits (MSB)
2. 一旦发现某位不等，两个数的大小关系就**已经确定**，忽略所有更低位的不等
### Cascading of Comparators
![Cascading of Comparators.png](/img/user/Cascading%20of%20Comparators.png)
## Encoder & Decoder
### Encoder
- **Input:** Accept an active level on one of its multiple input lines
- **Output:** Multiple output lines

> [!tip]
> 看哪一根线是亮的，它就把那根线的编号报出来。是“$2^n$ 进 → $n$ 出”

![Encoder.png](/img/user/Encoder.png)
#### Decimal-to-BCD Priority Encoder
Produce BCD output corresponding to the highest-order decimal digit input that's active & ignore any other lower-order active inputs
### Decoders
$N$ inputs, $2^N$ outputs

> [!tip]
> 给它一个编号，它就只点亮对应的那一根线。是“$n$ 进 → $2^n$ 出”。

**One-hot outputs:** Only 1 output active at once
![Decoder.png](/img/user/Decoder.png)

![Decoder Implementation.png](/img/user/Decoder%20Implementation.png)
#### Logic Using Decoders
OR the minterms
![OR the minterms.png](/img/user/OR%20the%20minterms.png)

## Multiplexer (MUX)
### Data Selector
- Select between one of $N$ inputs to connect to output
- Select input is $\log_2 N$ bits - Control input

| S（选择信号） | 输出 Y |
| ------- | ---- |
| 0       | A    |
| 1       | B    |

$Y = \bar{S}\cdot A + S\cdot B$
> [!tip]
> $S$ 是 0 就放 $A$ 过去，$S$ 是 1 就放 $B$ 过去


![Pasted image 20261030213436.png](/img/user/Pasted%20image%2020261030213436.png)

![Pasted image 20261030214111.png](/img/user/Pasted%20image%2020261030214111.png)
### Logic using MUX
- Lookup table
![Pasted image 20261030214522.png](/img/user/Pasted%20image%2020261030214522.png)
- Logic function generator
![Pasted image 20261030214551.png](/img/user/Pasted%20image%2020261030214551.png)
### Demultiplexer: Data Distributor
> [!tip]
> 只有一个入口，却有好几个出口。它根据控制信号，把进来的那一个信号“送到指定的某一个出口”，其余出口则保持不动（输出 0）

## Timing
**Delay:** Time between input change & output change
Caused by
- Capacitance & resistance in circuit
- Speed of light limitation
### Propagation & Contamination Delay
- **Propagation Delay:** $t_{pd}$ = max. delay form input to output
- **Contamination delay:** $t_cd$ = min. delay from input to output
 
 Reason of difference between $t_{pd}$ and $t_{cd}$:
 - Different rising & falling delays
 - Multiple inputs & outputs, some of which are faster
 - Circuits slow down when hot & speed up when cold
### Critical (Long) & Short Paths
![Pasted image 20261030215529.png](/img/user/Pasted%20image%2020261030215529.png)
### Glitches
Occur when a single input change causes an output to change multiple times