## Problem statement

There are `n` airports, labeled from `0` to `n - 1`, which are connected by some flights. You are given an array `flights` where `flights[i] = [from_i, to_i, price_i]` represents a one-way flight from airport `from_i` to airport `to_i` with cost `price_i`. You may assume there are no duplicate flights and no flights from an airport to itself.

You are also given three integers `src`, `dst`, and `k` where:

- `src` is the starting airport
- `dst` is the destination airport
- `src != dst`
- `k` is the maximum number of stops you can make (not including `src` and `dst`)

Return **the cheapest price** from `src` to `dst` with at most `k` stops, or return `-1` if it is impossible.

**Example 1:**

![](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/e272e71f-c38b-4db8-3c4e-1158418d2a00/public)

```java
Input: n = 4, flights = [[0,1,200],[1,2,100],[1,3,300],[2,3,100]], src = 0, dst = 3, k = 1

Output: 500
```

Copy

Explanation:  
The optimal path with at most 1 stop from airport 0 to 3 is shown in red, with total cost `200 + 300 = 500`.  
Note that the path `[0 -> 1 -> 2 -> 3]` costs only 400, and thus is cheaper, but it requires 2 stops, which is more than k.

**Example 2:**

![](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/93e910ee-378d-4ac8-93e0-471df7ccf600/public)

```java
Input: n = 3, flights = [[1,0,100],[1,2,200],[0,2,100]], src = 1, dst = 2, k = 1

Output: 200
```

Copy

Explanation:  
The optimal path with at most 1 stop from airport 1 to 2 is shown in red and has cost `200`.

**Constraints:**

- `1 <= n <= 100`
- `fromi != toi`
- `1 <= pricei <= 1000`
- `0 <= src, dst, k < n`
## Notes

- Use a variation of Bellman-Ford where we perform k + 1 breadth first searches from the origin node and update an array which stores the distance between destination node and origin node
- Every iteration from 1 to k + 1 we update the array which stores minimum distance
## Complexity

- Time: $O(k \cdot n)$
- Space: $O(n)$
## Code

```python
class Solution:

    def findCheapestPrice(self, n: int, flights: List[List[int]], src: int, dst: int, k: int) -> int:

        prices = [float("inf")] * n

        prices[src] = 0

  

        adj = {i : [] for i in range(n)}

  

        for flight in flights:

            src, dst, w = flight

            adj[src].append([dst, w])

  

        for i in range(k + 1):

            temp = prices.copy()

            for src, dst, w in flights:

                if prices[src] == float("inf"):

                    continue

                if prices[src] + w < temp[dst]:

                    temp[dst] = prices[src] + w

  

            prices = temp

  

        return -1 if prices[dst] == float("inf") else prices[dst]
```

#bellmanford
#graphs 