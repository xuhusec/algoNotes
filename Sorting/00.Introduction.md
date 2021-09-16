# Introduction

In computer science, a sorting algorithm is an algorithm that puts elements of a list into an order. The most frequently used orders are numerical order and lexicographical order, and either ascending or descending. Efficient sorting is important for optimizing the efficiency of other algorithms  (such as search and merge algorithms) that require input data to be in sorted lists. Sorting is also often useful for canonicalizing data and for producing human-readable output.

Formally, the output of any sorting algorithm must satisfy two conditions:

1. The output us in monotonic order (each element is no smaller/larger than the previous element, according to the required order).
2. The output is a permutation (a reordering, yet retaining all of the original elements) of the input.

For optimum efficiency, the input data should be stored in a data structure which allows random access rather than one that allows only sequential access.

### Common Sorting Algorithm

|                     | Best case |                                                              |
| ------------------- | --------- | ------------------------------------------------------------ |
| Comparison sort     | O(nlogn)  | A comparison sort is a type of sorting algorithms that only reads the list of elements through a single abstract comparison operation that determines which of two element should occur first in the final list |
| non-comparison sort | O(n)      | Usually for sorting of numbers. It is hard for storing strings or objects. Require additional space |

![sorting_at_a_glance](image\sorting_at_a_glance.png)

| Algorithm      | Avg    | Worst | Best  | Space complexity                                  | Stable |
| -------------- | ------ | ----- | ----- | ------------------------------------------------- | ------ |
| insertion sort | n^2^   | n^2^  | n     | O(1)                                              | Y      |
| shell sort     | n^1.3^ | n^2^  | n     | O(1)                                              | N      |
| selection sort | n^2^   | n^2^  | n^2^  | O(1)                                              | N      |
| heap sort      | nlogn  | nlogn | nlogn | O(n)\O(1) (if uses array itself as the heap O(1)) | N      |
| bubble sort    | n^2^   | n^2^  | n     | O(1)                                              | Y      |
| quick sort     | nlogn  | n^2^  | nlogn | nlogn                                             | N      |
| merge sort     | nlogn  | nlogn | nlogn | n                                                 | Y      |
|                |        |       |       |                                                   |        |
| counting Sort  | n + k  | n + k | n + k | n + k                                             | Y      |
| bucket sort    | n + k  | n^2^  | n     | n + k                                             | Y      |
| radix sort     | nk     | nk    | nk    | n + k                                             | Y      |

#### Simple Sort

##### Insertion Sort

Insertion sort is a simple sorting algorithm that is relatively efficient for small lists and mostly sorted lists, and is often used as part of more sophisticated algorithms. It works by taking elements from the list one by one and insert them in their corrected position into a new sorted list similar to how we put money in our wallet. In arrays, the new list and the remaining elements can share the array space, but insertion is expensive, requiring shifting all following element over by one.

##### Selection Sort

Selection sort is an in-place comparison sort. It has O(n^2^) complexity, making it inefficient on large lists and generally performs worse than the similar insertion sort. Selection sort is noted for its simplicity, and also has performance over more complicated algorithm in certain situations.

The algorithm finds the minimum value, swaps it with the value in the first position, and repeat theses steps for the reminder of the list.

##### Bubble Sort

Bubble sort is a simple sorting algorithm. The algorithm starts at the beginning of the data set. It compares the first two elements, and if the first is greater than the second. It swaps them, It continues doing this for each pair of adjacent elements to the end of the data set. It then starts again. with the first two elements repeating until no swaps have occurred on the last pass. This algorithm's average time and worst case performance is O(n^2^). So it is rarely used to sort large, unordered data set. Bubble sort can be used to sort a small number of items. Bubble sort can also be used efficiently on a list of any length that is nearly sorted.

#### Efficient Sort

##### Quick Sort

Quick Sort is a divide and conquer algorithm which relies on a partition operations to partition an array, an element called pivot is selected. All elements smaller than the pivot are moved before it and all greater elements are moved after it. This can be done efficiently in linear time and in-place. The lesser and greater sub-lists are then recursively sorted. This yields average time complexity of O(nlogn), with low overhead, and thus this is a  a popular algorithm. Efficient implementations of quick sort (with in-place partitioning) are typically unstable sorts and somewhat complex but are among the fastest sorting algorithms in practices. Together with its modest O(nlogn) space usage. Quicksort is one of the most popular sorting algorithms and is available in many standard programming libraries.  

##### Merge Sort

Merge Sort takes advantage of the ease of merging already sorted list. It starts by comparing every two elements and swapping them if the first should come after the second.  It then merges each of the resulting lists of two into lists of four, then merges those lists of four, and so on;  until at last two lists are merged into the final sorted list. The algorithm scales well to very large lists because its worst-case running time is O(nlogn). It is also easily applied to lists, not only arrays, as it only requires sequential access, not random access. However, it has additional O(n) space complexity, and involves a large number of copies in simple implementations.

Both merge sort and quicksort are divide and conquer algorithms.

| Algorithm  |                                                              |
| ---------- | ------------------------------------------------------------ |
| Merge Sort | Sort left and right sub array first and then merge them into sorted list |
| Quicksort  | Rearrange elements into left and right subarrays and then sort them individually |

 ##### Heap Sort

Heap Sort is much more efficient version of selection sort. It also works by determine the largest (or smallest) element of the list, placing that at the end (or beginning) of the list, then continuing with the rest of the list, but accomplishes this task efficiently by using a data structure called heap, a special type of binary tree. Once the data list has been made into heap, the root node is guaranteed to be the largest (or smallest) element. When it is removed and placed at the end of the list, the heap is rearranged so that the largest element remaining moves to the root. Using the heap, finding the next largest elements takes O(logn) time instead of O(n) for a linear scan as in simple selection sort. This allows heap sort to run in O(logn) time and this is also the worst case complexity.

  #### Distribution Sort

##### Counting Sort

Counting sort is applicable when each input is known the belong to a particular set, S, of possibilities. The algorithm runs in O(|S| + n) time and O(|S|) memory where n is the length of the input. It works by creating an integer array of size |S| and using the ith bin to count the occurrences of the ith bin member of S in the input. Each input is then counted by incrementing the value of its corresponding bin. Afterward, the counting array is looped though to arrange all of the input in order. This sorting algorithm is often cannot be used because S needs to be reasonably small for the algorithm to be efficient, but it is extremely fast and demonstrates great asymptotic behavior as n increases. It also can be modified to provide stable behavior.

##### Bucket Sort

Bucket Sort is a divide and conquer sorting algorithm. That generalize the counting sort by partitioning an array into a finite number of buckets. Each bucket is then sorted individually, either using a different sorting algorithm, or by reclusively applying the bucket sorting algorithm.

A bucket sort works best when the elements of the data set are evenly distributed across all buckets.

##### Radix Sort

Radix Sort is an algorithm that sorts numbers by processing individual digits. n numbers consisting of k digits each are sorted in O(nk) time. Radix Sort can process digits of each number either starting from the lest significant digit (LSD) or starting from the most signification digits (MSD). The LSD algorithm first sorts the list by the least significant digits while preserving their relative order using a stable sort. Then it sorts them by the next digit and so on from the least significant to the most significant, ending up with a sorted list. While the LSD radix sort requires the use of a stable sort, the MSD radix sort algorithm does not (unless stable sorting is desired). In-place MSD radix sort is not stable. It is common for the counting sort algorithm to be used internally by the radix sort. A hybrid sorting approach, such as using insertion sort for small bins, improves performance of radix sort significantly.



### Example of Implementations

#### Quick Sort

```java
public void sort(Comparable[] a) {
    quicksort(a, 0, a.length - 1);
}
private void quicksort(Comparable[] a, int lo, int hi) {
    if (lo >= hi) {
        return;
    }
    int pivot = partition(a, lo, hi);
    sort(a, lo, j - 1);
    sort(a, j + 1, hi);
}
private int partition(Comparable[] a, int lo, int hi) {
    int idx = lo;
    var pivot = a[hi];
    for (int i = lo; i < hi; ++i) {
        if (a[i].compareTo(pivot) < 0) { //assume there is no null element
            swap(a, i, idx++);
        }
    }
    swap(a, idx, hi);
    return idx;
}
private void swap(Comparable[] a, int i, int j) {
    var temp = a[i];
    a[i] = a[j];
    a[j] = temp;
}
```

#### Merge Sort

```java
public void sort(Comparable[] a) {
    Comparable[] temp = new Comparable[a.length];
    mergeSort(a, 0, a.length - 1, temp);
}

private void mergeSort(Comparable[] a, int lo, int hi, Comparable[] temp) {
    if (lo >= hi) {
        return;
    }
    int mid = lo + (hi - lo)/2;
    mergeSort(a, lo, mid, temp);
    mergeSort(a, mid + 1, hi, temp);
    merge(a, lo, mid, hi, temp);
}

private int merge(Comparable[] a, int lo, int mid, int hi, Comparable[] temp) {
    int i = lo;
    int j = mid + 1;
    int idx = lo;
    while (i <= mid && j <= hi) {
        temp[idx++] = a[i].compareTo(a[j]) < 0 ? a[i++] : a[j++];
    }
    while (i <= mid) {
        temp[idx++] = a[i++];
    }
    while (j <= hi) {
        temp[idx++] = a[j++];
    }
    while (lo <= hi) {
        a[lo] = temp[lo];
        lo++;
    }
}
```

#### Heap Sort

```java
public void sort(Comparable[] a) { 
    final int N = a.length;
    for (int i = N/2 - 1; i >= 0; --i) {
        heapify(a, N, i);
    }
    
    for (int i = n - 1; i > 0; --i) {
        swap(a, 0, i);
        heapify(a, i, 0);
    }
}
// To heapify a subtree rooted with node i and
// n is the size of the heap
private void heapify(Comparable[] a, int n, int i) {
    int largest = i;
    // get two children
    int l = 2 * i + 1;
    int r = 2 * i + 2;
    // if left child is lareger than root
    if (l < n && arr[l].compareTo(a[i]) > 0 ) {
        largest = l;
    }
    if (r < n && arr[r].compareTo(a[largest]) > 0 ) {
        largest = r;
    }
    
    // if larest is not root, rearrange the element
    if (largest != i) {
        swap(a, i, largest);
        
        heapify(arr, n, largest);
    }
}

private void swap(Comparable[] a, int i, int j) {
    var temp = a[i];
    a[i] = a[j];
    a[j] = temp;
}
```

Of course, you can use the standard library for the heap. But that would be extra space

```java
public void sort(Comparable[] a) {
    if (a.length < 1) { return; }
    PriorityQueue<Object> pq = new PriorityQueue<>()
    for(var e : a) {
        pq.add(e);
    }
    
    for (int i = 0; i < a.length; ++i) {
        a[i] = pq.poll();
    }
}
```

