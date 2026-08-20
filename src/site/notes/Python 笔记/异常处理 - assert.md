---
{"dg-publish":true,"permalink":"/python/assert/","tags":["Python异常处理"],"dg-note-properties":{"tags":["Python异常处理"]}}
---

>[!note] AI Usage Declaration
>本文基于 Qwen 3.7 Plus 内容修改

`assert` 语句用于测试一个条件是否必须为真。如果条件为真，程序继续执行；如果条件为假，则抛出 `AssertionError`（断言错误），并可选择附带错误信息。 
**语法**：`assert condition, "optional error message"`
``` python
def calculate_discount(price: float, discount_rate: float) -> float:
    # 内部逻辑检查：折扣率必须在 0 到 1 之间，这是函数内部的前提条件
    assert 0.0 <= discount_rate <= 1.0, f"折扣率必须在 0 到 1 之间，当前值为: {discount_rate}"
    
    return price * (1 - discount_rate)

# 正常调用
print(calculate_discount(100, 0.8))  # 输出: 20.0

# 触发断言错误
# print(calculate_discount(100, 1.5)) 
# 会抛出: AssertionError: 折扣率必须在 0 到 1 之间，当前值为: 1.5
```
>[!warning]
>**绝对不要**使用 `assert` 来验证外部输入（如用户输入、API 请求参数、文件读取等）
## 与 `raise` 的区别
| 特性          | `assert` (断言)                  | `raise` (抛出异常)                       |
| ----------- | ------------------------------ | ------------------------------------ |
| **主要目的**    | 内部逻辑检查、调试、防御性编程                | 异常控制流、错误处理、业务边界校验                    |
| **抛出的异常类型** | 固定为 `AssertionError`           | 任意 `Exception` 子类（内置或自定义）            |
| **能否被关闭**   | **能**（通过 `python -O` 优化模式）     | **不能**（永远生效）                         |
| **适用场景**    | 开发阶段、内部不变量检查、不可能到达的代码分支        | 生产环境、外部输入校验、API 边界、业务逻辑错误            |
| **调用者预期**   | 调用者**不应该**去 `try...except` 捕获它 | 调用者**应该**在适当层级 `try...except` 捕获并处理它 |

