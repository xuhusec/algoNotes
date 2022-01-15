## Reconstruct Itinerary

[link](https://leetcode.com/problems/reconstruct-itinerary/)

You are given a list of airline tickets where tickets[i] = [from<sub>i</sub>, to<sub>i</sub>] represent the departure and the arrival airports of one flight. Reconstruct the itinerary in order and return it.

All of the tickets belong to a man who departs from "JFK", thus, the itinerary must begin with "JFK". If there are multiple valid itineraries, you should return the itinerary that has the smallest lexical order when read as a single string.

* For example, the itinerary ["JFK", "LGA"] has a smaller lexical order than ["JFK", "LGB"].

You may assume all tickets form at least one valid itinerary. You must use all the tickets once and only once.

#### Hierholzer's Algorithm

This question is a simplified Eulerian path problem because the starting vertex is given. If that is not given it can be found by comparing indegree and outdegree.

The logical here is from the starting points keep visiting other nodes in dfs and remove the edges between nodes. If there is no cycle, the destination node would not point to other nodes firstly among all nodes.
The destination node might be visited multiple times but because there is no cycle and the edges are being removed. The final destination would be left first.
In other word the indegree of the final destination is larger than the outdegree of that node by 1. After removing that node, we can travel back to remove it previous one.
The order of visting nodes is the answer. But since we need to add the node backward. The destination is added first and the origin in added last. We need to either reverse the result or adding backward.

```java
    public List<String> findItinerary(List<List<String>> tickets) {
        // sorting by destination vertex so that the airport with smaller lexical name would be visited first
        Collections.sort(tickets, (a,b) -> a.get(1).compareTo(b.get(1)));
        // use Deque<String> to remove easily
        Map<String, Deque<String>> adj = new HashMap<>();
        // establish adjacent map
        for (List<String> ticket : tickets) {
            adj.computeIfAbsent(ticket.get(0), k -> new LinkedList<>()).add(ticket.get(1));
        }
        LinkedList<String> res = new LinkedList<>();
        //dfs
        dfs(adj, res, "JFK");
        // or you can use ArrayList and run the following method to reverse it
        //Collections.reverse(res);
        return res;
    }

    private void dfs(Map<String, Deque<String>> adj, Deque<String> res, String airport) {
        if (adj.containsKey(airport)) {
            Deque<String> nexts = adj.get(airport);
            while(!nexts.isEmpty()) {
                dfs(adj, res, nexts.removeFirst());
            }
        }
        //add current node to the front
        res.addFirst(airport);
        // you can also use ArrayList and here would be res.add(airport) and reverse the whole list before returning the result.
    }
```

Time complexity: dfs -> all Edges tickets.size(), let's say |E|. the sorting  -> |E|log|E| O(|E|log|E|).

Space complexity: adjacent map |V| key-value pair of the map and total |E| in all elements -> O(|V|+|E|).