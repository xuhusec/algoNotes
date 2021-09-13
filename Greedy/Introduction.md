# Introduction

Greedy

A greedy algorithm is a simple, intuitive algorithm that is used in optimization problems. The algorithm make the optimal choice at each step as it attempts to find the overall optimal way to solve the entire problem. It is any algorithm that follows the problem-solving heuristic of making the locally optimal choice at each stage. In many problems, a greedy strategy does not produce an optimal solution, but a greedy heuristic can yield locally optimal solutions that approximate a globally optimal solution in a reasonable amount of time.

Difference between Greedy and dynamic programming

* Greedy: make optimal choice at each step. no other scenario is considered
* DP: Keep the previous results, choose between them according to current condition. It  can make alternative choice at each step if the current one is not working. When the subproblem is small enough, it might be good enough for greedy but it one might need to consider several or all subproblems to get the optimal solutions for larger problems.
* backtrack: try different paths at each step

Application of Greedy Algorithm

* Huffman code

* minimum spanning tree