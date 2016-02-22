# Python data structures

## Stack

The list methods make it very easy to use a list as a stack, where the last
element added is the first element retrieved.

```python
stack = [3, 4, 5]
stack.append(6)
# stack
# [3, 4, 5, 6]
stack.pop() # 6
# stack
[3, 4, 5]
```

## Queue

To implement a queue, use `collections.deque` which was designed to have fast
appends and pops **from both ends**.

```python
from collections import deque
queue = deque()
queue.append("Eric")
queue.append("John")
# queue
# ["Eric", "John"]
queue.popleft() # Eric
# queue
# ['John']
```

## Heap

`import heapq`

There are 2 ways to create a heap

- `heappush()`
- `heapify()`

```python
import heapq
data = []
heapq.heappush(data, 4)
heapq.heappush(data, 6)
# data
# [4, 6], min is at the head
```

`heapq` implements a min-heap
