---
{"dg-publish":true,"permalink":"/python/raise-from/","tags":["Python异常处理"],"created":"2026-07-06T13:18:40.167+08:00","updated":"2026-08-20T14:23:55.358+08:00","dg-note-properties":{"tags":["Python异常处理"]}}
---

>[!note] AI Usage Declaration
>本文基于 Qwen 3.7 Plus 生成内容修改

当你在 `except` 块中触发新异常时，Python 会自动将正在处理的异常赋值给新异常的 `__context__` 属性。
但这只是隐式的，当你使用 `raise NewException from e` 时，Python 会将 `e` 赋值给新异常的 **`__cause__`** 属性。
- **`__context__` (隐式)**：“在处理上一个异常时，又发生了这个异常。”（语义较弱）
- **`__cause__` (显式)**：“上一个异常是导致这个异常的**直接原因**。”（语义强烈，Traceback 提示语也不同）
## 只使用 `raise` 不使用 `from` （隐形）
```python
def read_config_implicit():
    try:
        1 / 0  # 模拟底层 ZeroDivisionError
    except ZeroDivisionError as e:
        # 直接抛出新异常，没有使用 from
        raise ValueError("配置数据计算无效") 

read_config_implicit()

""" 
Output:
Traceback (most recent call last):
  File "main.py", line 3, in read_config_implicit
    1 / 0
ZeroDivisionError: division by zero

During handling of the above exception, another exception occurred:  <-- 注意这里的提示语

Traceback (most recent call last):
  File "main.py", line 8, in <module>
    read_config_implicit()
  ...
ValueError: 配置数据计算无效
"""
```
## 使用 `raise ... from e` （显式）
```python
def read_config_explicit():
    try:
        1 / 0  # 模拟底层 ZeroDivisionError
    except ZeroDivisionError as e:
        # 使用 from e 建立显式因果链
        raise ValueError("配置数据计算无效") from e

read_config_explicit()

"""
Output:
Traceback (most recent call last):
  File "main.py", line 3, in read_config_explicit
    1 / 0
ZeroDivisionError: division by zero

The above exception was the direct cause of the following exception:  <-- 注意这里的提示语变了！语义更明确

Traceback (most recent call last):
  File "main.py", line 8, in <module>
    read_config_explicit()
  ...
ValueError: 配置数据计算无效
"""
```
## 使用 `raise ... from None` 
``` python
def read_config_suppressed():
    try:
        1 / 0  # 模拟底层 ZeroDivisionError
    except ZeroDivisionError as e:
        # 使用 from None 刻意隐藏原始异常
        raise ValueError("配置数据计算无效") from None

read_config_suppressed()

"""
Output:
Traceback (most recent call last):
  File "main.py", line 8, in <module>
    read_config_suppressed()
  ...
ValueError: 配置数据计算无效
# (原始的 ZeroDivisionError 堆栈被完全隐藏了)
"""
