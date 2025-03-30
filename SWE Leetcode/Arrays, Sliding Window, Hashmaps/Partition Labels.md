## Problem statement

You are given a string `s`. We want to partition the string into as many parts as possible so that each letter appears in at most one part. For example, the string `"ababcc"` can be partitioned into `["abab", "cc"]`, but partitions such as `["aba", "bcc"]` or `["ab", "ab", "cc"]` are invalid.

Note that the partition is done so that after concatenating all the parts in order, the resultant string should be `s`.

Return _a list of integers representing the size of these parts_.

**Example 1:**

**Input:** s = "ababcbacadefegdehijhklij"
**Output:** `[9,7,8]`
**Explanation:**
The partition is "ababcbaca", "defegde", "hijhklij".
This is a partition so that each letter appears in at most one part.
A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits s into less parts.

**Example 2:**

**Input:** s = "eccbbbbdec"
**Output:** `[10]`

**Constraints:**

- `1 <= s.length <= 500`
- `s` consists of lowercase English letters.
## Notes

- Use hashmap to keep track of all last occurences
- Use two pointers to keep track of start and end of each partition
## Complexity

- Time: $O(n)$
- Space: $O(n)$
## Code

```python
class Solution:

    def partitionLabels(self, s: str) -> List[int]:

        m = {char: i for i, char in enumerate(s)}  

        res = []

        start, end = 0, 0  

  

        for i, letter in enumerate(s):

            end = max(end, m[letter])  # we find the last occurence of unique char

  

            if i == end:  # we have checked over every possible letter in this partition

                res.append(end - start + 1)

                start = i + 1

  

        return res
```

#medium 
#hashmap 
#twopointer
#arrays