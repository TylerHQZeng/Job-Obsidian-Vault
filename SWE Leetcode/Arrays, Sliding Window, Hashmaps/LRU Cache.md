## Problem statement

Design a data structure that follows the constraints of a **[Least Recently Used (LRU) cache](https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU)**.

Implement the `LRUCache` class:

- `LRUCache(int capacity)` Initialize the LRU cache with **positive** size `capacity`.
- `int get(int key)` Return the value of the `key` if the key exists, otherwise return `-1`.
- `void put(int key, int value)` Update the value of the `key` if the `key` exists. Otherwise, add the `key-value` pair to the cache. If the number of keys exceeds the `capacity` from this operation, **evict** the least recently used key.

The functions `get` and `put` must each run in `O(1)` average time complexity.

**Example 1:**

**Input**
`["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]`
`[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]`
**Output**
`[null, null, null, 1, null, -1, null, -1, 3, 4]`

**Explanation**
```
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // cache is {1=1}
lRUCache.put(2, 2); // cache is {1=1, 2=2}
lRUCache.get(1);    // return 1
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
lRUCache.get(2);    // returns -1 (not found)
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
lRUCache.get(1);    // return -1 (not found)
lRUCache.get(3);    // return 3
lRUCache.get(4);    // return 4
```

**Constraints:**

- `1 <= capacity <= 3000`
- `0 <= key <= 104`
- `0 <= value <= 105`
- At most `2 * 105` calls will be made to `get` and `put`.


## Initial thoughts

- Object could be a combo of a map and a deque where we insert elements into the deque and pop from the left when we hit the capacity
- However, this deque would need to be implemented with a doubly-linked list in order to optimize to $O(1)$ time on all operations

## Complexity:

- Time: $O(1)$ for all operations
- Space: $O(N)$ where $N$ is capacity

## Code

```python
from threading import Lock


class Node:
    def __init__(self, key=0, val=0, prev=None, next=None) -> None:
        self.key = key
        self.val = val
        self.prev = prev
        self.next = next
        
class LRUCache: 
    '''
    self.hmap:
        {key: Node(key, val, next, prev)}
    '''
    def __init__(self, capacity) -> None:
        if capacity < 0:
            raise ValueError('Capacity must be positive')
        self.capacity = capacity
        self.hmap = {}
        self.head = Node()
        self.tail = Node()
        self.head.next = self.tail
        self.tail.prev = self.head
        self.lock = Lock()


    def get(self, key):
        with self.lock:
            if key in self.hmap:
                self._move_to_head(self.hmap[key])
                return self.hmap[key].val
            
            return -1


    def put(self, key, value):
        with self.lock:
            if key in self.hmap:
                node = self.hmap[key]
                self._move_to_head(node)
                if value != node.val:
                    self.hmap[key].val = value
                    self.head.val = value
            else:
                if len(self.hmap) == self.capacity:
                    tail = self._pop_tail()
                    del self.hmap[tail.key]
                node = Node(key=key, val=value, next=self.head)
                self.hmap[key] = node
                self._add_head(node)


    def _move_to_head(self, node):
        self._remove_node(node)
        self._add_head(node)
        

    def _remove_node(self, node):
        prev_node = node.prev
        next_node = node.next
        prev_node.next = next_node
        next_node.prev = prev_node
    

    def _pop_tail(self):
        '''
        remove node before dummy tail
        '''
        node = self.tail.prev
        if node == self.head:
            return None
        self._remove_node(node)
        return node


    def _add_head(self, node):
        '''
        add a node after dummy head
        '''
        node.prev = self.head
        node.next = self.head.next
        self.head.next.prev = node
        self.head.next = node
        


# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```

#linkedlists
#medium 
#hashmap