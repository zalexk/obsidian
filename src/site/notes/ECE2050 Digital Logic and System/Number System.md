---
{"dg-publish":true,"permalink":"/ece-2050-digital-logic-and-system/number-system/","created":"2026-09-22T13:46:20.046+08:00","updated":"2026-10-13T17:31:41.223+08:00","dg-note-properties":{}}
---


## Binary Number System
这一节的内容可以用这个例子来总结
To express $(1001.1101)_{2}$ in decimal number,

| 1                 | 0                 | 0                 | 1                 | .   | 1                    | 1                       | 0                    | 1                         |
| ----------------- | ----------------- | ----------------- | ----------------- | --- | -------------------- | ----------------------- | -------------------- | ------------------------- |
| $1\times 2^3 = 8$ | $0\times 2^2 = 0$ | $0\times 2^1 = 0$ | $1\times 2^0 = 1$ |     | $1\times 2^{-1}=0.5$ | $1\times 2^{-2} = 0.25$ | $0\times 2^{-3} = 0$ | $1\times 2^{-4} = 0.0625$ |

Sum them up to get the decimal number of $(1001.1101)_{2} = 8+1 + 0.5+0.25+0.0625 = 9.8125$
## Octal and Hexadecimal Numbers
换算为十进制跟上面二进制换算一样，在此不述
- Least significant figure (LSD)
- Most significant figure (MSD)
### Conversion between Binary, Octal and Hexadecimal Numbers
规则为
- 3 个二进制为 1 个八进制
- 4 个二进制为 1 个十六进制
![Oct-Hex2Bin.png](/img/user/%E9%99%84%E4%BB%B6/Oct-Hex2Bin.png)
![Bin2Oct-Hex.png](/img/user/%E9%99%84%E4%BB%B6/Bin2Oct-Hex.png)
## Bytes and Nibbles

| Unit   | No. of Bits | Represent values per unit | Range     |
| ------ | ----------- | ------------------------- | --------- |
| Byte   | 8           | $2^8 = 256$               | $[0,255]$ |
| Nibble | 4           | $2^4 = 16$                | $[0,15]$  |

| Number Digit | No. of bit | No. of byte   | No. of nibble |
| ------------ | ---------- | ------------- | ------------- |
| Binary Digit | 1          | $\frac{1}{8}$ | $\frac{1}{4}$ |
| Octal Digit  | 3          | $\frac{3}{8}$ | $\frac{3}{4}$ |
| Hex          | 4          | $\frac{1}{2}$ | 1             |


## Signed Numbers
### Sign / Magnitude Numbers
- **Positive number:** sign bit = 0
- **Negative number:** sign bit = 1
**Range:** $[-(2^{N-1}-1), 2^{N-1}-1]$
**Example**
- +6 = 0110
- -6 = 1110
### Two's Complement Numbers
- **Positive number:** sign bit = 0
- **Negative number:** sign bit = 1
**Range:** $[-2^{N-1}, 2^{N-1}-1]$
**Step:**
1. Convert to one's complement: `0` 和 `1` 互换
2. Add 1

**Example:** Calculate two's complement of $-3$
1. **Binary number of 3:** $0011$
2. **One's complement:** $1100$
3. **Add 1:** $1101$
Hence, the two's complement of $-3$ is `1101`
> [!tip]
> 只有当 sign bit 一致的情况下才有可能会出现 overflow error

- **Subtraction:** 转换为加法，如 $5-3 \Rightarrow 5+(-3)$
- **Multiplication:** 按一般乘法做
- **Division:** 不断做 subtraction
> [!note] Example
>> Divide $01100100$ by $00011001$
> 1. Convert $00011001$ to 2's complement (negation 变成负数)
> 	1. $00011001 \to 11100111$
> 2. 不断做 subtraction
> 	1. $01100100 + 11100111 = 01001011$
> 	2. $01001011 + 11100111 = 00110010$ 
> 	3. $00110010 + 11100111 = 00011001$
> 	4. $00011001 + 11100111 = 00000000$ 
> 3. Quotient = $4 = (0100)_2$

## Fixed-Point Number
定点数 fixed-point number 就是固定小数点的位置
### Unsigned Fixed Point Formats
$Ua.b$
- $a$ is integer bit
- $b$ is fraction bit

> [!note] Example
> **Convert 6.75 into binary**
> $$
> \begin{aligned}
> 6 &= (110)_{2} \\
> 0.75 &= (0.11)_{2}
> \end{aligned}
> $$
> Represent 6.75 in different format:
> - $U4.4 = \underbrace{0110}_{6} \underbrace{1100}_{0.75}$
> - $U 3.5 = \underbrace{110}_{6} \underbrace{11000}_{0.75}$
> - $U 6.2 = \underbrace{000110}_{6} \underbrace{11}_{0.75}$

### Signed Fixed Point Format
$Qa.b$: signed 2's complement number
- $a$ is integer bit, including the sign bit
- $b$ is fraction bit
Convert the unsigned fixed point format to 2's complement
> [!note] Example
> Write -6.75 in Q4.4
> 1. $6.75 = (01101100)_2$
> 2. 1's complement: $10010011$
> 3. Add 1 LSB: $10010100$

### Saturating Arithmetic
定点溢出 Fixed point overflow 通常很糟糕，会产生难看的伪影（artifacts）：
- 视频里明亮区域中间出现暗像素
- 音频里出现咔哒声
**Saturating Arithmetic:** Use largest value when overflow

> [!note] Example
> In U4.4, $11000000+01111000 = 100111000$
> Overflow error occurs
> Hence, use the largest value of U4.4 under saturating arithmetic, i.e. $11000000+01111000 = 11111111$
## Floating Point Numbers
类似科学计数法 (General form: $\pm M \times B^E$)
- $M$ = 尾数 mantissa
- $B$ = Base
- $E$ = Exponent
We use IEEE 754 floating-point standard
- 1 bit for sign
- 8 bit for biased exponent
- 23 bit for fraction

### Biased Exponent
Range of exponent (without biased): $[0, 2^8-1] = [0,255]$
只能表示正数和 0，表示不了负数
但是科学计数法里的指数是有正有负，因此把 exponent 全部加 127，变成 positive number 储存
$$
\begin{aligned}
\text{存进格子的值} &=\text{真实指数} + \text{偏移量(bias)} \\
\text{取出时：真实指数} &= \text{格子里的值} - \text{偏移量}
\end{aligned}
$$ 
> [!note] Example
> Represent 228 using 32 bit floating point representation
> 1. **Convert to binary number:** $228 = (11100100)_2$
> 2. **Normalize (把小数点移到第二位):** $11100100 = 1.1100100 \times 2^7$
> 	- 移动几位，指数就是几。这里移了 7 位 → 指数 $E = 7$
> 3. 计算 sign bit, exponent and mantissa
> 	1. **Sign bit:** 0
> 	2. **Exponent:** $7 + 127 = 134 = (10000110)_{2}$
> 	3. **Mantissa / Fraction:** 由于第一位（即小数点前的那位）永远为 1，所以可以省略来减省空间
> 		1. 保存为 $1100100$ 
> 		2. 由于 fraction bit 是 23-bit 长，因此要填充 $0$，因此为 $110\;0100\;0000\;0000\;0000\;0000$
> 
> 因此，$228 = 0\;10000110\;11001000000000000000000$


> [!note] Example
> Write -58.25 in floating point
> 1. **Convert to binary number:** $58.25 = (111010.01)_2$
> 2. **Normalize:** $1.1101001 \times 2^5$
> 3. Fill the fields
> 	1. **Sign bit:** 1
> 	2. **Exponent bit:** $5+127 = 132 = (10000100)_2$
> 	3. **Fraction bit:** $110\ 1001\ 0000 \ 0000 \ 0000\ 0000$

### Special Cases
| Number            | Sign | Exponent | Fraction |
| ----------------- | ---- | -------- | -------- |
| 0                 | X    | 00000000 | 全 0      |
| $+\infty$         | 0    | 11111111 | 全 0      |
| $-\infty$         | 1    | 11111111 | 全 0      |
| NaN（Not a Number） | X    | 11111111 | 非 0      |

## Non-positional / Non-weighted Number System
并非所有二进制串都是用来做算术的"数"，有些只是**编码（code）**
- **位置/加权计数系统（positional/weighted number system）：** 符号的值由它的位置决定
	- e.g. 十进制、二进制、八进制、十六进制
- **非位置/非加权系统（non-positional/non-weighted）：** 符号的值与位置无关
	- e.g. 格雷码（Gray Code）、循环码（cyclic code）
## Binary Coded Decimal (BCD)
把每一个十进制数字单独用一个 4 位二进制编码表示
例如 8421 code
![BCD(8421 code).png](/img/user/%E9%99%84%E4%BB%B6/BCD(8421%20code).png)

#### BCD Addition
Add two BCD numbers （跟二进制加法一致）
- If a 4-bit sum $\le$ 9, it is valid BCD number
- Else, add 6 $(0110)_2$ to 4-bit sum
![BCD Addition.png](/img/user/%E9%99%84%E4%BB%B6/BCD%20Addition.png)
> [!note]
> 4 bit 二进制的 range 是 $[0,15]$，但 BCD 的 range 是 $[0,9]$（到 1001 = 9 就该进位了）
> 加 6 正好把这段落差补回来，让进位时序重新和十进制对齐

## Gray Code
Only a single bit change from one code word to the next in sequence 
相邻的 Gray Code 只有 1 bit 的变化
![Gray Code.png](/img/user/%E9%99%84%E4%BB%B6/Gray%20code.png)
Denote each digit of Gray Code by $G_i$ and digit of binary number by $B_i$
- Convert from binary number to Gray Code
	1. Copy MSB (最左边的数字, i.e. $G_1 = B_1$)
	2. XOR: $G_i = B_i \oplus B_{i-1}$

> [!note] Example
> Convert the binary number $1100\ 0110$ to Gray Code
> 1. $G_1 = B_{1} = 1$
> 2. Carry out XOR operation
> $$
> \begin{aligned}
> G_{2} &= B_{2} \oplus B_{1} = 1 \oplus 1 = 0 \\
> G_{3} &= B_{3} \oplus B_{2} = 0 \oplus 1 = 1 \\
> G_{4} &= B_{4} \oplus B_{3} = 0 \oplus 0 = 0 \\
> G_{5} &= B_{5} \oplus B_{4} = 0 \oplus 0 = 0 \\
> G_{6} &= B_{6} \oplus B_{5} = 1 \oplus 0 = 1 \\
> G_{7} &= B_{7} \oplus B_{6} = 1 \oplus 1 = 0 \\
> G_{8} &= B_{8} \oplus B_{7} = 0 \oplus 1 = 1
> \end{aligned}
> $$
> Hence, the Gray Code is $10100101$.

- Convert from Gray Code to binary number
	- Copy MSB (i.e. $B_1 = G_{1}$)
	- XOR: $B_i = B_{i-1} \oplus G_i$

> [!note] Example
> Convert Gray Code $10101111$ to binary number.
> $$
> \begin{aligned}
> B_1 &= G_{1} = 1 \\
> B_{2} &= B_{1} \oplus G_{2} = 1 \oplus 0 = 1 \\
> B_{3} &= B_{2} \oplus G_{3} = 1 \oplus 1 = 0 \\
> B_{4} &= B_{3} \oplus G_{4} = 0 \oplus 0 = 0 \\
> B_{5} &= B_{4} \oplus G_{5} = 0 \oplus 1 = 1 \\
> B_{6} &= B_{5} \oplus G_{6} = 1 \oplus 1 = 0 \\
> B_{7} &= B_{6} \oplus G_{7} = 0 \oplus 1 = 1 \\
> B_{8} &= B_{7} \oplus G_{8} = 1 \oplus 1 = 0
> \end{aligned}
> $$
> Hence, the binary number is $11001010$.

## Error Codes
数据在传输或存储中可能出错（由 0 变 1 或反之）
### Parity Bit for Error Detection
- **Even parity code:** `1` 的数量是 even
- **Odd parity code:** `1` 的数量是 odd
只有当错的 bit 数量为 odd 才可以检测到
### Cyclic Redundancy Check (CRC)
CRC 是能检测数据块中**多个错误**的检错方法：
- **发送端：** 对数据块计算出一个校验和（checksum），附在数据后面一起发送；
- **接收端：** 用同样的方法重新计算校验和并比对
结果为 0 说明未检出差错，非 0 说明出错。
> [!note] Example
> Given 
> - Data: $10110010$
> - Generator code: $1010$
> Denote Data by $D$ and Generator code by $G$
> 
> **Send**
> 1. 在 data 后添加 $(n-1) = 3$ 个 $0$ （n 是 Generator code 的长度）
> 	$D' =1011\ 0010 \ 000$
> 2. Modulo-2 Division: $\frac{D'}{G} = 110$
> 3. Append the remainder / checksum to $D$
> 	The transmitted CRC is $10110010110$
> 
> **Receive**
> Divide received data by generator code
> - **Correct:** Remainder = 0
> - **Error:** Remainder is non-zero
![CRC.png](/img/user/%E9%99%84%E4%BB%B6/CRC.png)






