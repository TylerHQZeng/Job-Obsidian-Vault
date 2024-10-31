## Problem statement

Given an `m x n` matrix `board` where each cell is a battleship `'X'` or empty `'.'`, return _the number of the **battleships** on_ `board`.

**Battleships** can only be placed horizontally or vertically on `board`. In other words, they can only be made of the shape `1 x k` (`1` row, `k` columns) or `k x 1` (`k` rows, `1` column), where `k` can be of any size. At least one horizontal or vertical cell separates between two battleships (i.e., there are no adjacent battleships).

**Example 1:**

![](https://assets.leetcode.com/uploads/2024/06/21/image.png)

**Input:** board = `[["X",".",".","X"],[".",".",".","X"],[".",".",".","X"]]`
**Output:** 2

**Example 2:**

**Input:** board = `[["."]]`
**Output:** 0

**Constraints:**

- `m == board.length`
- `n == board[i].length`
- `1 <= m, n <= 200`
- `board[i][j]` is either `'.'` or `'X'`.

**Follow up:** Could you do it in one-pass, using only `O(1)` extra memory and without modifying the values `board`?
## Notes

- For the followup just check if the previous row or col contains an "X" or is the first row or first column,
## Complexity

- Time: $O(n)$
- Space: $O(n)$
## Code

```python
class Solution:

    def countBattleships(self, board: List[List[str]]) -> int:

        count = 0

        for row in range(len(board)):

            for col in range(len(board[0])):

                if board[row][col] == "X" and (row == 0 or board[row - 1][col] == ".") and (col == 0 or board[row][col - 1] == "."):

                    count += 1

        return count
```

#matrix
#arrays 
#dfs
