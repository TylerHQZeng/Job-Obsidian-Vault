## Problem statement

Given the `root` of a binary tree with unique values and the values of two different nodes of the tree `x` and `y`, return `true` _if the nodes corresponding to the values_ `x` _and_ `y` _in the tree are **cousins**, or_ `false` _otherwise._

Two nodes of a binary tree are **cousins** if they have the same depth with different parents.

Note that in a binary tree, the root node is at the depth `0`, and children of each depth `k` node are at the depth `k + 1`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/02/12/q1248-01.png)

**Input:** root = `[1,2,3,4]`, x = 4, y = 3
**Output:** false

**Example 2:**

![](https://assets.leetcode.com/uploads/2019/02/12/q1248-02.png)

**Input:** root = `[1,2,3,null,4,null,5]`, x = 5, y = 4
**Output:** true

**Example 3:**

![](https://assets.leetcode.com/uploads/2019/02/13/q1248-03.png)

**Input:** root = `[1,2,3,null,4]`, x = 2, y = 3
**Output:** false

**Constraints:**

- The number of nodes in the tree is in the range `[2, 100]`.
- `1 <= Node.val <= 100`
- Each node has a **unique** value.
- `x != y`
- `x` and `y` are exist in the tree.
## Notes

- Use BFS and add each node's depth and parent to a hashmap
- Check if the two nodes have same depth but different parent
## Complexity

- Time: $O(n)$
- Space: $O(n)$
## Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isCousins(self, root: Optional[TreeNode], x: int, y: int) -> bool:
        m = {}
        q = deque([(root, TreeNode(-1), 0)])

        while q:
            node, parent, depth = q.popleft()
            m[node.val] = [parent, depth]
            if node.left:
                q.append((node.left, node, depth + 1))
            if node.right:
                q.append((node.right, node, depth + 1))
        
        if x not in m or y not in m:
            return False
        c1, c2 = m[x], m[y]
        if c1[1] == c2[1] and c1[0] != c2[0]:
            return True
        return False
```

#trees 
#bfs 
#dfs 
#hashmap 
#easy