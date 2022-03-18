# 数据结构与算法

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


### Queue傻瓜版

```python3
class Queue:

    def __init__(self):
        self.data = []

    def push(self, value):
        self.data.append(value)

    def pop(self):
        return self.data.pop(0)

    def top(self):
        return self.data[0]

    def is_empty(self):
        return len(self.data) == 0
```

### Queue

```python3
class Queue:

    class Node:
        def __init__(self, elem, next=None):
            self.elem = elem
            self.next = next

    def __init__(self):
        self.tail = None

    def push(self, value):
        '''
        >>> queue = Queue()
        >>> queue.push(1)
        >>> queue.push(2)
        >>> queue.pop()
        1
        >>> queue.pop()
        2
        '''
        if self.tail:
            self.tail.next = Queue.Node(value, self.tail.next)
            self.tail = self.tail.next
        else:
            self.tail = Queue.Node(value, None)
            self.tail.next = self.tail

    def pop(self):
        head = self.tail.next
        value = head.elem
        if head is self.tail:
            self.tail = None
        else:
            self.tail.next = head.next
        return value

    def is_empty(self):
        return not self.tail
```

