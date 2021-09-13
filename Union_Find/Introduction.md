# Introduction

In computer science, a disjoint-set data structure, also called a union-find data structure or merge-find set, is a data structure that stores a collection of disjoint (non-overlapping) sets, Equivalently, it stores a partition of a set into disjoint subsets. It provides operations for adding new sets, merging sets ( replacing them by their union), and finding a representative member of a set. The last operation allows to find out efficiently if any two elements are in the same or different set. It is often applied to grouping questions.

Operations

| Operations    | Description                                                  |
| ------------- | ------------------------------------------------------------ |
| makeSet(s)    | Create a new disjoint set with s element(s)                  |
| uninSet(x, y) | combine the set containing x, saying Set A, and the set containing y, saying set B, if no common element belongs to both A and B. Otherwise, A and B are kept the same (Actually we already have A == B at this point). |
| find(x)       | find the representative member of the set containing x. This is very helpful to decide if two elements are in the same set by comparing their representative member. |

Initialization

At the beginning, every node points itself as its parent node 

![initialization](image\uf_init.png)

Merge

Merge two different sets. Point one root node to another. Usually, we point the one with less elements to the other. This would reduce the work of path compress, which would be shown next.

![merge](image\uf_merge.png)

Path Compression

During the find, we would compress the paths. The height of the tree is reduced. We make any non-root nodes in the path as direct child of the root node.

![path compression](image\uf_pc.png)

Example of implementation

```java
public class UnionFind {
    int[] parents;
    // a rank number of elements in the tree
    // we only maintain the cound at root node
    int[] ranks;
    UnionFind(int n) {
        parent = new int[n];
        ranks = new int[n];
        for (int i = 0; i < n; ++i) {
            parent[i] = i;
            ranks[i] = 1;
        }
    }
    public int find(int x) {
        if (parent[x] != x) {
            //path compression
            parent[x] = find(parent[x]);
        }
        return parent[x];
    }
    public void merge(int x, int y) {
        int pX = find(x);
        int pY = find(y);
        if (pX == pY) {
            return;
        }
        if (ranks[pX] > ranks[pY]) {
            parent[pY] = pX;
            ranks[pX] += ranks[pY];
        } else {
            parent[pX] = pY;
            ranks[pY] += ranks[pX];
        }
    }
}
```

