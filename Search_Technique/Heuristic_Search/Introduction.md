# Introduction

Heuristic is a technique designed for solving a problem more quickly when classic methods are too slow, or for finding an approximate solution when classic methods fail to find any exact solution. This is achieved by trading optimality, completeness, accuracy, or precision for speed. In a way, it can be considered a shortcut.

A heuristic function, also simply called a heuristic, is a function that ranks alternatives in search algorithms at each branching step based on available information to decide which branch to follow.

Initially, the heuristic tries every possibility at each step, like the full-space search algorithm. But it can stop the search at any time if the current possibility is already worse than the best solution already found. In such search problems, a heuristic can be used to try good choices first so that bad paths can be eliminated early. In this case of best-first search algorithms, such as A* search, the heuristic improves the algorithm's convergence while maintaining its correctness as long as the heuristic admissible. 

## A* algorithm

A* is a graph traversal and path search algorithm, which is often used in many fields of computer science due to its completeness, optimality, and optimal efficiency. One major practical drawback is its O(b^d^) space complexity, as it stores all generated nodes in memory. Thus, in practical travel-routing systems, it is generally outperformed by algorithms which can pre-process the graph to attain better performance, as well as memory-bounded approaches; however, A* is still the best solution in many cases.

A* is an informed search algorithm, or a best-first search, meaning that it is formulated in terms of weighted graphs: starting from a specific starting node of a graph, it aims to find a path to the given goal node having the smallest cost. IT does this by maintaining a tree of paths originating at the start node and extending those paths one edge at a time until its termination criterion is satisfied.



At each iteration of its main loop, A* needs to determine which of its paths to extend. It does so based on the cost of the path and an estimate of the cost required to extend the path all the way to the goal. Specifically, A* selects the path the minimizes

f(n) = g(n) + h(n)

where n is the next node on the path, g(n) is the cost of the path from the start node to n, and the h(n) is a heuristic function that estimates the cost of the cheapest path from n to the goal. A* terminates when the path it chooses to extend is a path from start to goal or if there are no path eligible to be extended. The heuristic function is problem-specific. If the heuristic function is admissible. meaning that it never overestimates the actual cost to get the goal, A* is guaranteed to return a least -cost path from start to goal.

Typical implementations of A* use a priority queue to perform the repeated selection of minimum (estimated) cost nodes to expand.

Example of A*

```java
public class Graph {
    private Vertex[] vertices;
    private List<Edge>[] adj;
    public Graph(Vertex[] vertices, Edge[] edges) {
        this.vertices = vertices;
        adj = new List[vertices.length];
        for (Edge e : edges) {
            if (adj[e.sid] == null) {
                adj[e.sid] = new ArrayList<>();
            }
            adj[e.sid].add(e);
        }
    }
    public int[] aStar(int src, int dest) {
        //reconstruct the path
        int[] predecessor = new int[vertices.length];
        // sort by f(n) = g(n) + h(n)
        PriorityQueue<Vertex> queue = new PriorityQueue<>(vertices.length, (v1, v2) -> v1.f - v2.f);
        boolean[] visited = new boolean[vertices.length];

        vertices[src].dist = 0;
        vertices[src].f = 0;

        queue.add(vertices[src]);
        visited[src] = true;

        while(!queue.isEmpty()) {
            Vertex minV = queue.poll();
            if (adj[minV.id] == null) {
                continue;
            }
            for (Edge e : adj[minV.id]) {
                Vertex next = vertices[e.tid];
                if (minV.dist + e.w < next.dist) {
                    next.dist = minV.dist + e.w;
                    next.f = next.dist + h(next, vertices[dest]);
                    predecessor[next.id] = minV.id;
                    if(visited[next.id]){
                        update(queue, next);
                    } else {
                        queue.add(next);
                        visited[next.id] = true;
                    }
                }
                if (next.id == dest) {
                    queue.clear();
                    break;
                }
            }
        }
        return predecessor;
    }

    private void update(PriorityQueue<Vertex> pq, Vertex v) {
        //unfortunately Java PriorityQueue does not support update.
        // we need to remove and reinsert to get.
        pq.remove(v);
        pq.add(v);
        // An example of pq with the ability to update the priority can be found at https://github.com/stanfordnlp/CoreNLP/blob/main/src/edu/stanford/nlp/util/BinaryHeapPriorityQueue.java#L376
        // https://algs4.cs.princeton.edu/24pq/IndexMinPQ.java.html
        // https://stackoverflow.com/a/714873
    }

    private int h(Vertex v1, Vertex v2) {
        // Manhattan distant
        return Math.abs(v1.x - v2.x) + Math.abs(v1.y - v2.y);
    }

    public static class Vertex {
        int id;
        //this distance between current node and the src
        //it is the g(n) of f(n) = g(n) + h(n)
        int dist;
        //the f(n) to be minimized in A*
        int f;
        //coordinates
        int x;
        int y;

        public Vertex(int id, int x, int y) {
            this.id = id;
            this.x = x;
            this.y = y;
            this.f = Integer.MAX_VALUE;
            this.dist = Integer.MAX_VALUE;
        }


    }

    public static class Edge {
        // start vertex
        int sid;
        // end vertex
        int tid;
        //weight
        int w;
        public Edge(int sid, int tid, int w) {
            this.sid = sid;
            this.tid = tid;
            this.w = w;
        }
    }
}
```



