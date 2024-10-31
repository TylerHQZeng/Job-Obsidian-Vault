## Problem statement

Given an `m x n` grid of characters `board` and a string `word`, return `true` _if_ `word` _exists in the grid_.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/04/word2.jpg)

**Input:** board = `[["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]]` word = "ABCCED"
**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg)

**Input:** board = `[["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]]`, word = "SEE"
**Output:** true

**Example 3:**

![](https://assets.leetcode.com/uploads/2020/10/15/word3.jpg)

**Input:** board = `[["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]]`, word = "ABCB"
**Output:** false

**Constraints:**

- `m == board.length`
- `n = board[i].length`
- `1 <= m, n <= 6`
- `1 <= word.length <= 15`
- `board` and `word` consists of only lowercase and uppercase English letters.

**Follow up:** Could you use search pruning to make your solution faster with a larger `board`?
## Notes

- Use DFS and backtracking to explore all different options starting from the first letter
## Complexity

- Time:$O(m * n * 4^{L})$
- Space: $O(1)$
## Code

```python
class Solution:

    def exist(self, board: List[List[str]], word: str) -> bool:

        directions = [(1,0),(-1,0),(0,1),(0,-1)]

        m, n = len(board), len(board[0])

  

        def dfs(row, col, i):

            if i == len(word):

                return True

            if (row < 0 or row >= m or col < 0 or col >= n or

                board[row][col] != word[i]):

                return False

  

            temp = board[row][col]

            board[row][col] = '#'  

            for dr, dc in directions:

                if dfs(row + dr, col + dc, i + 1):

                    board[row][col] = temp  

                    return True

  

            board[row][col] = temp  

            return False

  

        for r in range(m):

            for c in range(n):

                if dfs(r, c, 0):

                    return True

  

        return False
```


# Followup

**Follow up:** Could you use search pruning to make your solution faster with a larger `board`?

- Check if the required amount of characters are even on the board before we begin dfs
- Can stop if the amount of valid grid cells left on the board is smaller than the remaining word
- Prioritize the path where the next character is
- 

#backtracking
#graphs 
#dfs 
#medium