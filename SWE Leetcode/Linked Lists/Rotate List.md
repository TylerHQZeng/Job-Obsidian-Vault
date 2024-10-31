## Problem statement

  
Code

Testcase

Test Result

Test Result

[61. Rotate List](https://leetcode.com/problems/rotate-list/)

Medium

Topics

Companies

Given the `head` of a linked list, rotate the list to the right by `k` places.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/13/rotate1.jpg)

**Input:** head = `[1,2,3,4,5]`, k = 2
**Output:** `[4,5,1,2,3]`

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/13/roate2.jpg)

**Input:** head = `[0,1,2]`, k = 4
**Output:** `[2,0,1]`

**Constraints:**

- The number of nodes in the list is in the range `[0, 500]`.
- `-100 <= Node.val <= 100`
- `0 <= k <= 2 * 109`
## Notes

- Use a slow and fast pointer and once we set the fast pointer to the kth element from the right, we set the right 
- Create a circular set and cut off the link at the kth index
## Complexity

- Time: $O(n)$
- Space: $O(1)$
## Code

```python
# Definition for singly-linked list.

# class ListNode:

#     def __init__(self, val=0, next=None):

#         self.val = val

#         self.next = next

class Solution:

    def rotateRight(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:

        if not head:

            return None

        temp = head

        length = 1

        while temp.next:

            temp = temp.next

            length += 1

  

        k = k % length

        temp.next = head

        temp = head

        for _ in range(length - k - 1):

            temp = temp.next

        answer = temp.next

        temp.next = None

        return answer
```


#linkedlists 
#medium 
