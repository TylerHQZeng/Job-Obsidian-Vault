## Problem statement

Given two strings `s` and `goal`, return `true` _if and only if_ `s` _can become_ `goal` _after some number of **shifts** on_ `s`.

A **shift** on `s` consists of moving the leftmost character of `s` to the rightmost position.

- For example, if `s = "abcde"`, then it will be `"bcdea"` after one shift.

**Example 1:**

**Input:** s = "abcde", goal = "cdeab"
**Output:** true

**Example 2:**

**Input:** s = "abcde", goal = "abced"
**Output:** false

**Constraints:**

- `1 <= s.length, goal.length <= 100`
- `s` and `goal` consist of lowercase English letters.
## Notes

- Concat the goal string together and check if s is in the goal string
## Complexity

- Time: $O(n)$
- Space: $O(n)$
## Code

```python
class Solution:

    def rotateString(self, s: str, goal: str) -> bool:

        concat = goal + goal

        if len(goal) != len(s):

            return False

        return s in concat
```

#strings 
#easy