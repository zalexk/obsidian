---
{"dg-publish":true,"permalink":"/python/enumerate/","dg-note-properties":{}}
---


格式：`enumerate(iterable, start=0)`
## 示例
### 常规输出
```python
>>> seasons = ['Spring', 'Summer', 'Fall', 'Winter']
>>> list(enumerate(seasons))
[(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]
>>> list(enumerate(seasons, start=1))       # 下标从 1 开始
[(1, 'Spring'), (2, 'Summer'), (3, 'Fall'), (4, 'Winter')]
```

### 与 `dict` 配合
```python
# 字典的 enumerate
person = {"name": "Tom", "age": 20, "city": "Beijing"}

# 遍历字典的键值对（需要 items）
for index, (key, value) in enumerate(person.items()):
    print(f"{index}: {key} = {value}")
"""
0: name = Tom
1: age = 20
2: city = Beijing
"""


# 创建带序号的字典
items = ["a", "b", "c"]
numbered = {i+1: v for i, v in enumerate(items)}
print(numbered)  # 输出: {1: 'a', 2: 'b', 3: 'c'}
```
## Reference
- [Python3 enumerate () 函数 | 菜鸟教程](https://www.runoob.com/python3/python3-func-enumerate.html)
- [Python enumerate() 函数 | 菜鸟教程](https://www.runoob.com/python/python-func-enumerate.html "Python enumerate() 函数 | 菜鸟教程")

