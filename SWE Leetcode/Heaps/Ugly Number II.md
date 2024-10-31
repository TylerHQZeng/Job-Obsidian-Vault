## Problem statement

An **ugly number** is a positive integer whose prime factors are limited to `2`, `3`, and `5`.

Given an integer `n`, return _the_ `nth` _**ugly number**_.

**Example 1:**

**Input:** n = 10
**Output:** 12
**Explanation:** `[1, 2, 3, 4, 5, 6, 8, 9, 10, 12]` is the sequence of the first 10 ugly numbers.

**Example 2:**

**Input:** n = 1
**Output:** 1
**Explanation:** 1 has no prime factors, therefore all of its prime factors are limited to 2, 3, and 5.
## Notes

- Use a heap to keep track of order, and use set to keep track of elements that have already been seen
- Each iteration heap push the top element multiplied by 2, 3, 5. This ensures the elements in the heap only have 2, 3, 5 as prime factors
## Complexity

- Time: $O(n)$
- Space: $O(n)$
## Code

```python
import heapq

  

class Solution:

    def nthUglyNumber(self, n: int) -> int:

        k = 0

        pq = [1]

        res = []

        seen = {1}

  

        while k < n:

            curr_small = heapq.heappop(pq)

            res.append(curr_small)

            if curr_small * 2 not in seen:

                heapq.heappush(pq, curr_small * 2)

                seen.add(curr_small * 2)

  

            if curr_small * 3 not in seen:

                heapq.heappush(pq, curr_small * 3)

                seen.add(curr_small * 3)

  

            if curr_small * 5 not in seen:

                heapq.heappush(pq, curr_small * 5)

                seen.add(curr_small * 5)

  

            k += 1

  

        return res[-1]
```

#heaps 
#math 
#medium 
#hashmap