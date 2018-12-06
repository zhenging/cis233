### Abstract Data Type
* Collection Interface. Iterator
* Stack. push/pop
* Queue. enqueue/dequeue
* LinkedList
	* Doubly-Linked List,
	* Circular Linked List

### Sorting Algorithms
insertion sort, shellsort, mergesort, quicksort (quickselect), heapsort



#### Shell Sort


#### Merge Sort
* Procedures
	1. If the number of items to sort is 0 or 1, return
	2. Recursively sort the first and second  halves seperately
	3. Merge the two sorted halves into a sorted group. (Done in linear time)
* Performance
Merge sort uses divide-and-conquer to obtain $O(N\lg N)$ running. However, it requires extra memory to merge two sorted sub lists. The additional work involved in copying to the temporary array and back and that slows the sort considerably.

#### Quick Sort
+ Procedures
1. If the number of elements is $S$ is 0 or 1, then return.
2. Pick any element $v$ in $S$. It called the **pivot**
3. Partition $S-\{v\}$(the remaining elements in S$S$) into two disjoint groups: $L = \{x\in S-\{v\} | x \le v\}$ and $R = \{x\in S-\{v\} | x \ge v\}$
4. Return the result of *Quicksort(L)* followed by $v$ followed by *Quicksort(R)*

+ Performance
	* The best case occurs when the partition always splits into equal subsets. The running time is $O(N \lg N)$.
	* The worse case occurs when the partition repeatedly generates an empty subset. The running time is $O(N^2)$.
	* The average case is $O(N \lg N)$.


* Quick Select

+ Picking a pivot
	* The first element (in position *low*). Wrong way.
	* The middle element *((low+right)/2)*. Reasonable but passive.
	* Median-of-three. Attempt to pick a better than average pivot.

* Heap Sort

### HashTable
+ How hashing function works?
+ Strategies to resolve collision
	* Linear Probing
	* Quadratic Probing
	*

### Trees
+ Basic Concepts - node, edge, root, parent, children, leaves, height,
+ Tree Traversal and Iterator
	* Preorder. Root -> left -> right
	* Inorder. Left -> root -> right.
	* Postorder. Left -> right -> root.

### Binary Search Tree

#### AVL tree

#### Red-black tree

#### B-tree

### Priority Queue and Heaps

#### Graph Algorithm
