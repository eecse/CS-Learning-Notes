# 基于Python的数据结构与算法学习

## 基本的数据结构实现

### Stack

```python3
class Stack:

    def __init__(self):
        self.data = []

    def push(self, value):
        self.data.append(value)

    def pop(self):
        return self.data.pop()

    def top(self):
        return self.data[-1]

    def is_empty(self):
        return len(self.data) == 0
```

