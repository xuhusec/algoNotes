# Introduction

In computer science, binary search, also known as half-interval search, logarithmic search, or binary chop, is a search algorithm that finds the position of a target value within a sorted array. Binary search compares the target value to the middle element of the array, If they are not equal, the half in which the target cannot lie is eliminated and the search continues on the remaining half, again taking the middle element to compare to the target value, and repeating this until the target value is found, If the search ends with the remaining half being empty, the target is not in the array.

Binary search runs in logarithmic time in the worst case, making O(logn) comparisons, where n is the number of elements in the array. Binary search is faster than liner search except for small arrays. However, the array must be sorted first to be able to apply binary search. There are specialized data structures designed for fast searching, such as hash tables, that can be searched more efficiently than binary search. However, binary search can be used to solve a wider range of problems, such as finding the next-smallest or next largest element in the array relative to the target even if it is absent from the array.

In summary, the following are the prerequisites of binary search

*  sorted data (monotonic increasing or monotonic decreasing)
* bounded data on both ends (known lower bound and upper bound)
* If data is stored in a data structure, the data structure should support random access (for a given indices)

Here is an example.

```java
// return the index of the arr, where arr[index] == target
// return -1 if no such element
public int binarySearch(int[] arr, int target) {
    if (arr == null || arr.length < 1) {
        return -1;
    }
    int lo = 0;
    int hi = arr.length - 1;
    // lo <= hi because the element may not exist;
    while (lo <= hi) {
        // find the middle element
        // we do not use (lo + hi)/2 because it may cause an overflow for two large indices
        int mid = lo + (hi - lo)/2;
        if (arr[mid] > target) {
            // if the element greater the the target
            // throw out the larger half in the array
            hi = mid - 1;
        } else if (arr[mid] < target) {
            // if the element lower the the target
            // throw out the smaller half in the array
            lo = mid + 1;
        } else {
            // find the target arr[mid] == target
            return mid;
        }
    }
    // does not find a match
    return -1;
}
```

