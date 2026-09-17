---
{"dg-publish":true,"permalink":"//fibonacci-sequence/","created":"2026-09-17T23:17:18.847+08:00","updated":"2026-09-17T23:40:37.401+08:00","dg-note-properties":{}}
---


## Question
Fibonacci sequence is
$$
f(n) = \begin{cases}
1 \quad &n<2 \\
f(n+1) + f(n+2) &n\geq 2
\end{cases}
$$
### Input
Input is integer $n$ ($0\le n \le 1000$)
### Output
Since $f(n)$ can be really big, hence output $f(n) \mod 998244353$
## Answer
### 递归（失败）
每次教到递归都会教如何用其来解 Fibonacci sequence
```python
def fib(n: int) -> int:
	MOD = 998244353
    if n >= 2:
        return (fib(n-1) + fib(n-2)) % MOD
    return 1
print(fib(int(input(""))))
```
但是这个算法复杂度为 $O(2^n)$，如果 $n$ 太大的话提交到 OJ 会失败
### 迭代
用回最传统的方法反而可以解题
``` python
def fib(n: int) -> int:
	MOD = 998244353
    if n < 2:
        return 1
    prev, now = 1, 1
    for _ in range(2, n + 1):
        prev, now = now, (prev + now) % MOD
    return now
    
print(fib(int(input())))
```
有一点需要注意的是，`prev, now = now, (prev + now) % MOD` 不可以分开写
``` python
# 错误示范
prev = now
now = (prev + now) % MOD
```
这样写的话，第二行的 `prev` 便成为 `now` 的值
``` python
now = (prev + now) % MOD
# 等价于
now = (now + now) % MOD
```

因此 `prev, now` 必须要写在同一行

#### C++ 版本
```c++
#include <iostream>
using namespace std;

long fib(int n) {
    long MOD = 998244353;
    if (n<2) return 1;
    long prev = 1, now = 1;
    for (int i = 2; i<=n; i++){
        long temp = now;
        now = (prev + now) % MOD;
        prev = temp;
    }
    return now;
}

int main(){
    int num;
    cin >> num;
    cout << fib(num);
}
```
