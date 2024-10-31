## Problem statement

We are given an array `asteroids` of integers representing asteroids in a row.

For each asteroid, the absolute value represents its size, and the sign represents its direction (positive meaning right, negative meaning left). Each asteroid moves at the same speed.

Find out the state of the asteroids after all collisions. If two asteroids meet, the smaller one will explode. If both are the same size, both will explode. Two asteroids moving in the same direction will never meet.

**Example 1:**

**Input:** asteroids = `[5,10,-5]`
**Output:** `[5,10]`
**Explanation:** The 10 and -5 collide resulting in 10. The 5 and 10 never collide.

**Example 2:**

**Input:** asteroids = `[8,-8]`
**Output:** `[]`
**Explanation:** The 8 and -8 collide exploding each other.

**Example 3:**

**Input:** asteroids = `[10,2,-5]`
**Output:** `[10]`
**Explanation:** The 2 and -5 collide resulting in -5. The 10 and -5 collide resulting in 10.

**Constraints:**

- `2 <= asteroids.length <= 104`
- `-1000 <= asteroids[i] <= 1000`
- `asteroids[i] != 0`
## Notes

- Iterate through all the asteroids from left to right, append each asteroid to the stack
- Every iteration check if the stack has any asteroid collisions and alter the stack accordingly
## Complexity

- Time: $O(n)$
- Space: $O(n)$
## Code

```python
class Solution:

    def asteroidCollision(self, asteroids: List[int]) -> List[int]:

        stack = []

  

        for i in range(len(asteroids)):

            stack.append(asteroids[i])

  

            while len(stack) > 1:

                a1, a2 = stack.pop(), stack.pop() # a1 is the one on the right, a2 is on the left

  

                if (a1 > 0 and a2 > 0) or (a1 < 0 and a2 < 0):

                    stack.append(a2)

                    stack.append(a1)

                    break

                if a1 > 0 and a2 < 0:

                    stack.append(a2)

                    stack.append(a1)

                    break

                if a1 < 0 and a2 > 0 and abs(a1) != abs(a2):

                    new_asteroid = a1 if abs(a1) > abs(a2) else a2

                    stack.append(new_asteroid)

  

        return stack
```

#medium 
#stack