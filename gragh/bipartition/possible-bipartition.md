# Possible Bipartition

Given a set of`N` people (numbered`1, 2, ..., N`), we would like to split everyone into two groups of **any **size.

Each person may dislike some other people, and they should not go into the same group.

Formally, if`dislikes[i] = [a, b]`, it means it is not allowed to put the people numbered `a`and `b`into the same group.

Return`true` if and only if it is possible to split everyone into two groups in this way.

```
1 <= N <= 2000
0 <= dislikes.length <= 10000
1 <= dislikes[i][j] <= N
dislikes[i][0] < dislikes[i][1]
There does not exist i != j for which dislikes[i] == dislikes[j].
```

## Example

**Example 1:**

```
Input: 
N = 4, dislikes = [[1,2],[1,3],[2,4]]
Output: true
Explanation: group1 [1,4], group2 [2,3]
```

**Example 2:**

```
Input: N = 3, dislikes = [[1,2],[1,3],[2,3]]
Output: false
```

**Example 3:**

```
Input: N = 5, dislikes = [[1,2],[2,3],[3,4],[4,5],[1,5]]
Output: false
```

## Note

相比之前拿道题，多了一个建图的预处理

## Code

```java
class Solution {
    public boolean possibleBipartition(int N, int[][] dislikes) {
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i <= N; i++) {
            graph.add(new ArrayList<>());
        }
        for (int[] elem : dislikes) {
            graph.get(elem[0]).add(elem[1]);
            graph.get(elem[1]).add(elem[0]);
        }

        int[] color = new int[N + 1];
        Queue<Integer> q = new LinkedList<>();
        //Divide the node in two sets such that no two nodes in same set are linked
        //[[1,2,3], [0,2], [0,1,3], [0,2]]
        for (int i = 1; i <= N; i++) {
            if (color[i] == 0) {
                q.offer(i);
                color[i] = 1;
                while (!q.isEmpty()) {
                    int node = q.poll();
                    for (int child : graph.get(node)) {
                        if (color[child] == 0) {
                            if (color[node] == 2) {
                                color[child] = 1;
                            } else {
                                color[child] = 2;
                            }
                            q.offer(child);
                        } else if (color[child] == color[node]) {
                            return false;
                        }                  
                    }
                }
            }
        }
        return true;
    }
}
```
