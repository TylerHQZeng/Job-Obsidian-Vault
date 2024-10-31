## Problem statement

Given a string `s`, return _the maximum number of unique substrings that the given string can be split into_.

You can split string `s` into any list of **non-empty substrings**, where the concatenation of the substrings forms the original string. However, you must split the substrings such that all of them are **unique**.

A **substring** is a contiguous sequence of characters within a string.

**Example 1:**

**Input:** s = "ababccc"
**Output:** 5
**Explanation**: One way to split maximally is `['a', 'b', 'ab', 'c', 'cc']`. Splitting like `['a', 'b', 'a', 'b', 'c', 'cc']` is not valid as you have 'a' and 'b' multiple times.

**Example 2:**

**Input:** s = "aba"
**Output:** 2
**Explanation**: One way to split maximally is `['a', 'ba']`.

**Example 3:**

**Input:** s = "aa"
**Output:** 1
**Explanation**: It is impossible to split the string any further.

**Constraints:**

- `1 <= s.length <= 16`
    
- `s` contains only lower case English letters.
## Notes

- Loop through all substrings in the recursive call and if it is not already in a set then add it and recurse and then remove to do the backtracking
## Complexity

- Time: $O(n * 2^{n})$
- Space: $O(n)$
## Code

```python
class Solution:

    def maxUniqueSplit(self, s: str) -> int:

        def dfs(word, seen):

            if len(word) == 0:

                return 0

            max_splits = 0

            for i in range(1, len(word) + 1):

                substring = word[:i]

                if substring not in seen:

                    seen.add(substring)

                    max_splits = max(max_splits, 1 + dfs(word[i:], seen))

                    seen.remove(substring)

            return max_splits

  

        return dfs(s, set())
```

#backtracking 
#dp 
#strings 
#medium