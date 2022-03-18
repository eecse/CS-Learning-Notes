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

### Priority Queue

```python3
class PriorityQueue:

    def __init__(self, max=True):
        self.data = []
        import operator
        self.cmp = operator.gt if max else operator.lt

    def push(self, priority, item):
        self.data.append((priority, item))
        self.up(len(self.data) - 1)

    def pop(self):
        self.data[0], self.data[-1] = self.data[-1], self.data[0]
        value = self.data.pop()[1]
        self.down(0)
        return value

    def top(self):
        return self.data[0][1]

    def is_empty(self):
        return len(self.data) == 0

    def up(self, pos):
        while pos:
            parent_pos = (pos - 1) >> 1
            if not self.cmp(self.data[pos][0], self.data[parent_pos][0]):
                break
            self.data[parent_pos], self.data[pos] = self.data[pos], self.data[parent_pos]
            pos = parent_pos

    def down(self, pos):
        limit = len(self.data)
        highest_priority = pos
        while pos < limit:
            left_child_pos = (pos << 1) + 1
            if left_child_pos < limit and self.cmp(self.data[left_child_pos][0], self.data[pos][0]):
                highest_priority = left_child_pos
            right_child_pos = (pos << 1) + 2
            if right_child_pos < limit and self.cmp(self.data[right_child_pos][0], self.data[highest_priority][0]):
                highest_priority = right_child_pos
            if highest_priority == pos:
                break
            self.data[highest_priority], self.data[pos] = self.data[pos], self.data[highest_priority]
            pos = highest_priority

    def __iter__(self):
        while not self.is_empty():
            yield self.pop()

pq = PriorityQueue(max=False)
assert pq.is_empty()
data = list(range(10))
import random
random.shuffle(data)
for i in data:
    pq.push(i, i)

output = [v for v in pq]
assert output == sorted(data)
```