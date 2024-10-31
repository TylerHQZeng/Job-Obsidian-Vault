## Problem statement

Given the `root` of a binary tree, return _the zigzag level order traversal of its nodes' values_. (i.e., from left to right, then right to left for the next level and alternate between).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

**Input:** root = `[3,9,20,null,null,15,7]`
**Output:** `[[3],[20,9],[15,7]]`

**Example 2:**

**Input:** root = `[1]`
**Output:** `[[1]]`

**Example 3:**

**Input:** root = []
**Output:** []

**Constraints:**

- The number of nodes in the tree is in the range `[0, 2000]`.
- `-100 <= Node.val <= 100`
## Notes

- Use breadth first search and keep track of the depth, if we are on even depth append left to right, else right to left
## Complexity

- Time: $O(n)$
- Space: $O(n)$
## Code

```python
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def zigzagLevelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:

        if not root:

            return []

        q = deque([(0, root)])

        res = []

  

        while q:

            length = len(q)

            temp = [None] * length

            for i in range(length):

                depth, node = q.popleft()

  

                if node.left:

                    q.append((depth + 1, node.left))

                if node.right:

                    q.append((depth + 1, node.right))

  

                if depth % 2 == 0:

                    temp[i] = node.val

                else:

                    temp[length - i - 1] = node.val

            res.append(temp)

  

        return res

```

#medium 
#bfs
#trees