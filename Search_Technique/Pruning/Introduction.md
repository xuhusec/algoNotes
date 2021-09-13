# Introduction

Pruning is a data compression technique in machine learning and search algorithms that reduces the size of decision trees by removing sections of the tree that are non-critical and redundant to classify instances. Pruning reduces the complexity of the final classifier, and hence improves predictive accuracy by the reduction of overfitting.

Although we are not talking about machine learning here, pruning is an important concept to improve performance. During this process, the redundant work is avoid instead of checking at the end. It is very common in the backtrack algorithm but we can apply this concept in other problem as well.

For example, in the N-Queens problem, we have either boolean set or mask to restrict where the next queue would be put instead of checking at the end to see if all queens cannot attack each other. If we do not limit the move, it would be O(n^n^) n rows with n columns. Each row would be n choices. But when we limit it, says with a set, it would be O(n!). After set the first row, only n-1 choices left and so on.





