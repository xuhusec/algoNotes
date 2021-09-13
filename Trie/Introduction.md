# Introduction

In computer science, a trie, also called digital tree or prefix tree, is a type of search tree, a tree data structure used for locating specific keys from within a set. These keys are most often strings, with links between nodes defined not by the entire key, but by individual characters. In order to access a key (to recover its value, change it, or remove it), the trie is traversed depth-first, following the links between nodes which represent each characters in the key.

 ![trie](image\trie.png)

Trie tree improve string comparison from hash table. It is often applied to statistics and sorting of massive strings. e.g. text analysis in search engine.

1. The node is not the entire key
2. the entire key is the aggregation of all values from the root node to the node with an ending flag.
3. Each child of a node represents a different character

One can also put some additional info in each node such as frequency of a word in the leaf node.

![trie_imp](image\trie_imp.png)

The above image illustrate how Trie is implemented. Each Node contains an array or a map of children. This is an N-ary tree. It is usually 26 to represents all lower case English character but in our example we have 52 to match the previous example with capital A . And a Node would have a mark to tell if this is a end of a key. In our example, that is the black square at the end. If it is back. then this is the end of a key. Please note that  the end of a key does not have to be the leaf node. Such as the in and inn.  The first n is not the leaf but it is the end of a key. 

Trie is another example of time space trade-off. This reduce searching time with common prefix.