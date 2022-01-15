## Valid Arrangement of Pairs

[link](https://leetcode.com/problems/valid-arrangement-of-pairs/)

You are given a 0-indexed 2D integer array pairs where pairs[i] = [start<sub>i</sub>, end<sub>i</sub>]. An arrangement of pairs is valid if for every index i where 1 <= i < pairs.length, we have end<sub>i-1</sub> == start<sub>i</sub>.

Return any valid arrangement of pairs.

Note: The inputs will be generated such that there exists a valid arrangement of pairs.

#### Hierholzer's Algorithm

This question is also Eulerian path problem. We can use the same idea from Problem 332. But in this problem we need to find out the origin first.
For the origin. If there is no cycle, it satisfies indegree - 1 = outdegree. Similarly, the destination satisfies indegree + 1 = outdegree. In this problem, we only need the origin
If the whole graph is a cycle, we can choose any points as the origin. Since hierholzer's algorithm would keep remove edges during dfs. The cycle would be broken.

In this problem, the Hierholzer would gives us the Eulerian path for vertexes, and we can reconstruct pair based on vertexes.
```java
    public int[][] validArrangement(int[][] pairs) {
        // maps to record indegrees and outdegrees
        Map<Integer, Integer> indegrees = new HashMap<>();
        Map<Integer, Integer> outdegrees = new LinkedHashMap<>();
        // adjacent map
        Map<Integer, Deque<Integer>> adj = new HashMap<>();
        // record indegrees and outdegrees and establish adjacent map
        for (int[] pair : pairs) {
            indegrees.merge(pair[1], 1, (v1, v2) -> v1 + v2);
            outdegrees.merge(pair[0], 1, (v1, v2) -> v1 + v2);
            adj.computeIfAbsent(pair[0], k -> new LinkedList<>()).add(pair[1]);
        }
        //find the origin
        Integer start = null;
        //Do not use indegrees to iterate because the origin might not have indegrees
        for (Map.Entry<Integer, Integer> entry : outdegrees.entrySet()) {
            if (entry.getValue() - 1 == indegrees.getOrDefault(entry.getKey(), 0)) {
                start = entry.getKey();
                break;
            }
        }

        // there is cycle, choose the first one
        if (start == null) {
            start = pairs[0][0];
        }

        Deque<Integer> list = new LinkedList<>();
        dfs(adj, start, list);

        int[][] res = new int[pairs.length][2];
        res[0][0] = list.removeFirst();
        res[0][1] = list.removeFirst();

        int id = 1;
        while (!list.isEmpty()) {
            res[id][0] = res[id - 1][1];
            res[id++][1] = list.removeFirst();
        }
        return res;
    }
    //Hierholzer's Algorithm
    private void dfs(Map<Integer, Deque<Integer>> adj, Integer start, Deque<Integer> queue) {
        if (adj.containsKey(start)) {
            Deque<Integer> edges = adj.get(start);
            while(!edges.isEmpty()) {
                dfs(adj, edges.removeLast(), queue);
            }
        }
        queue.addFirst(start);
    }
```

Time complexity: construct indegrees and outdegrees and adjacent map -> O|E|. finding the origin O(|V|) dfs -> all Edges O(|E|), O(|V| + |E|).

Space complexity:  indegrees and outdegrees and adjacent map -> O(|V|+|E|).