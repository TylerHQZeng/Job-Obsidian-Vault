## Problem statement

A parentheses string is valid if and only if:

- It is the empty string,
- It can be written as `AB` (`A` concatenated with `B`), where `A` and `B` are valid strings, or
- It can be written as `(A)`, where `A` is a valid string.

You are given a parentheses string `s`. In one move, you can insert a parenthesis at any position of the string.

- For example, if `s = "()))"`, you can insert an opening parenthesis to be `"(**(**)))"` or a closing parenthesis to be `"())**)**)"`.

Return _the minimum number of moves required to make_ `s` _valid_.

**Example 1:**

**Input:** s = "())"
**Output:** 1

**Example 2:**

**Input:** s = "((("
**Output:** 3

**Constraints:**

- `1 <= s.length <= 1000`
- `s[i]` is either `'('` or `')'`.
## Notes

- Use a stack to keep track of open parantheses. If there is a match, pop off the stack. 
- If the we encounter that the stack is empty and we hit a right parantheses, we know we are missing an opening bracket so add one
- Add the length of the stack after iterating through the string; this accounts for all missing closing parantheses
## Complexity

- Time: $O(n)$
- Space: $O(n)$
## Code

```python
class Solution:

    def minAddToMakeValid(self, s: str) -> int:

        stack = []

        res = 0

        for p in s:

            if p == "(":

                stack.append("(")

            elif p == ")":

                if len(stack) > 0:

                    stack.pop()

                else:

                    res += 1

  

        res += len(stack)

        return res
```

#stack 
#medium