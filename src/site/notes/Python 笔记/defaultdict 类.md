---
{"dg-publish":true,"permalink":"/python/defaultdict/","created":"2026-06-12T12:24:46.639+08:00","updated":"2026-08-20T14:24:11.896+08:00","dg-note-properties":{}}
---


**特点：** key 不存在时会返回默认值，而不会报错
- If key exists, return its value
- If key D.N.E., return default value
	- **int:** returns `0`
	- **list:** returns `[]`
	- **str:** returns `""`
## 示例
```python
from collections import defaultdict
d = defaultdict(int)

d['apple'] = 5
print(d)
print(d['juices'])

"""
Output:
defaultdict(<class 'int'>, {'apple': 5})
0
"""
```
