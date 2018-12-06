### 08 Sorting Algorithms

#### Insertion

##### Procedures
  1. Consider the first element to be sorted.
  2.  Iterate the array from $2$nd elements to the last one.  Compare $a[i]$ with $a[i-1]$, if $a[i]>a[i-1]$, done; otherwise, find the correct position within $1$th to $i-1$th elements(which is sorted), shift all the larger values up to make a space, and insert $a[i]$ into that correct position.

```java
void insertionSort(int arr[]) {
  for (int i = 1; i < arr.length; i ++) {
    int key = arr[i];
    int j = i;

    while (j > 0 && arr[j - 1] > key) {
      arr[j] = a[j - 1];
      j--;
    }

    a[j] = key;
  }
}
```

##### Performance
The insertion sort is quadratic in the average and worst case. It is fast if the inout has already been sorted.


#### Shellsort

##### Procedures
Shell's idea was to avoid the large amount of data movement, first by comparing elements that were far apart and then by comparing elements that were less far apart, and so on, gradually shrinking toward the basic insertion sort. (*Diminishing Gap Sort*)

```java
void shellsort(int arr[]) {
  for (int gap = a.length / 2; gap > 0; gap = gap == 2? 1: (int)(gap / 2.2)) {
    for (int i = gap; i < a.length; i ++) {
      int temp = a[i];
      int j = i;

      while (j >= gap && a[j-gap] > temp) {
        a[j] = a[j-gap];
        j -= gap;
      }

      a[j] = temp;
    }
  }
}
```

##### Performance
1. Shell sort is a subquadratic algorithm and highly dependent on the increment sequence, which is an improvement over the insertion sort.
2. In worst case, Shell's increments give *quadratic* behavior. ($N$ is an exact power of 2, all the large elements are in even-indexed array positions, and all the small elements are in odd-index array positions.)
3. If consecutive increments share no common factors, a worst case running time of at most $O(N^{3/2})$ will be achieved.
4. Dividing by $2.2$ gives excellent performance in practice.

#### Mergesort

##### Procedures
1. If the number of items to sort is 0 or 1, return
2. Recursively sort the first and second  halves seperately
3. Merge the two sorted halves into a sorted group. (Done in linear time)

##### Performance
Merge sort uses divide-and-conquer to obtain $O(N\lg N)$ running. However, it requires extra memory to merge two sorted sub lists. The additional work involved in copying to the temporary array and back and that slows the sort

#### Quicksort

##### Quickselect
