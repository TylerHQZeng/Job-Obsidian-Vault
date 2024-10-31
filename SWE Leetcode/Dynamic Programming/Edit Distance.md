## Problem statement

Given two strings `word1` and `word2`, return _the minimum number of operations required to convert `word1` to `word2`_.

You have the following three operations permitted on a word:

- Insert a character
- Delete a character
- Replace a character

**Example 1:**

**Input:** word1 = "horse", word2 = "ros"
**Output:** 3
**Explanation:** 
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')

**Example 2:**

**Input:** word1 = "intention", word2 = "execution"
**Output:** 5
**Explanation:** 
intention -> inention (remove 't')
inention -> enention (replace 'i' with 'e')
enention -> exention (replace 'n' with 'x')
exention -> exection (replace 'n' with 'c')
exection -> execution (insert 'u')

**Constraints:**

- `0 <= word1.length, word2.length <= 500`
- `word1` and `word2` consist of lowercase English letters.
## Notes

- If the length of the two words are different, we can simply return the difference
- Our DFS function takes in two parameters, one for the index of the first word and the second one for the index of the second word
- We return the minimum between:

```python
dfs(i + 1, j),    # delete
dfs(i, j + 1),    # insert
dfs(i + 1, j + 1) # replace
```

## Complexity

- Time: $O(m * n)$ where $m,n$ are the lengths of word1 and word2
- Space: $O(m*n)$
## Code

```python
class Solution:

    def minDistance(self, word1: str, word2: str) -> int:

        @cache

        def dfs(i, j):

            if i == len(word1):

                return len(word2) - j

            if j == len(word2):

                return len(word1) - i

            if word1[i] == word2[j]:

                return dfs(i + 1, j + 1)

            return 1 + min(

                dfs(i + 1, j),    # delete

                dfs(i, j + 1),    # insert

                dfs(i + 1, j + 1) # replace

            )

        return dfs(0, 0)
```

#dp 
#medium 
#hard