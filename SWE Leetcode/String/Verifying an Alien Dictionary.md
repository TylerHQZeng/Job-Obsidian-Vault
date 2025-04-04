## Problem statement

In an alien language, surprisingly, they also use English lowercase letters, but possibly in a different `order`. The `order` of the alphabet is some permutation of lowercase letters.

Given a sequence of `words` written in the alien language, and the `order` of the alphabet, return `true` if and only if the given `words` are sorted lexicographically in this alien language.

**Example 1:**

**Input:** words = `["hello","leetcode"]`, order = "hlabcdefgijkmnopqrstuvwxyz"
**Output:** true
**Explanation:** As 'h' comes before 'l' in this language, then the sequence is sorted.

**Example 2:**

**Input:** words = `["word","world","row"]`, order = "worldabcefghijkmnpqstuvxyz"
**Output:** false
**Explanation:** As 'd' comes after 'l' in this language, then words`[0]` > words`[1]`, hence the sequence is unsorted.

**Example 3:**

**Input:** words = `["apple","app"]`, order = "abcdefghijklmnopqrstuvwxyz"
**Output:** false
**Explanation:** The first three characters "app" match, and the second string is shorter (in size.) According to lexicographical rules "apple" > "app", because 'l' > '∅', where '∅' is defined as the blank character which is less than any other character ([More info](https://en.wikipedia.org/wiki/Lexicographical_order)).

**Constraints:**

- `1 <= words.length <= 100`
- `1 <= words[i].length <= 20`
- `order.length == 26`
- All characters in `words[i]` and `order` are English lowercase letters.
## Notes

- Use hash map to store the new lexicographic ordering
## Complexity

- Time: $O(n \cdot m)$ where $n$ is the number of words and $m$ is the length of the word
- Space: $O(n)$
## Code

```python
class Solution:

    def isAlienSorted(self, words: List[str], order: str) -> bool:

        order_map = {char: idx for idx, char in enumerate(order)}

  

        for i in range(len(words) - 1):

            w1, w2 = words[i], words[i + 1]

  

            for c1, c2 in zip(w1, w2):

                if order_map[c1] < order_map[c2]:

                    break

                if order_map[c1] > order_map[c2]:

                    return False

            else:

                if len(w1) > len(w2):

                    return False

  

        return True
```

#easy
#hashmap 
#strings