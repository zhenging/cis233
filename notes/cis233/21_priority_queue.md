### 21 A Priority Queue: The Binary Heap

#### Priority Queue
+ The priority queue supports access of **the minimum item** only.
+ We want to be able to **access** the smallest item in a collection of items and **remove** it from the collection. (`findMin()` and `deleteMin()`).
+ The binary heap implements the priority queue in **logarithmic time** per operation with litter extra space.
+ `heapsort` runs in $O(N \log N)$ time but uses **no extra memory**.

E.g.
+ Printer jobs. (Several 1-page jobs and one 100-page job, it might be reasonable to print the long job last, even if it is not the last job submitted.)
+ Multiuser environment. Operating system scheduler. (Short jobs that use fewer resources should have precedence over jobs that have already consumerd large amounts of resources).
+ Event-driven simulation

#### Heap
+ The heap is a _complete binary tree_, allowing representation by a simple array (_implicit representation_) and guaranteeing logarithmic depth.
+ Every node except the root has a parent. The _parent_ is in position $\lfloor i/2 \rfloor$, the _left child_ is in position $2i$, and the _right child_ is in position $2i + 1$.
+ In a heap, for every node $X$ with parent $P$, the key in $P$ is smaller than or equal to the key in $X$.
+ The root's parent in position $0$ is given a value of negative infinity.

#### Allowed Operations And Implementation

##### Insertion
+ Insertion is implemented by creating a hole at the next available location adn then **percolating it up** util the new item can be placed in it without introducting a heap order violation with the hole's parent.
+ The time required to do the insertion could be as much as $O(N \log N)$ if the element to be inserted is the new minimum. The reason is that it will percolate up all the way to the root. On average the percolation terminates early: It has been shown that $2.6$ comparisons are required on average to perform the add, so the average add moves and element up $1.6$ levels.

```java
public boolean add(AnyType x) {
  if (currentSize + 1 == array.length) {
    doubleArray();
  }

  // percolate up
  int hole = ++currentSize;
  array[0] = x;
  for (; compare(x, array[hole / 2]) < 0; hole /= 2) {
    array[hole] = array[hole / 2];
  }
  array[hole] = x;

  return true;
}
```

##### The `deleteMin` Operation
+ Deletion of the minimum involves placing former last item in a hold that is created at the root. The hole is **percolated down** through minimum children until the item can be placed without violating the heap-order property.
+ The `deleteMin` operation is logarithmic in both the worst and average cases.

```java
public AnyType remove() {
  AnyType minItem = element();
  array[1] = array[currentSize --];
  percolateDown(1);

  return minItem;
}

private void percolateDown(int hole) {
  int child;
  AnyType tmp = array[hole];

  for (; hole * 2 <= currentSize; hole = child) {
    child = hole * 2;

    // find smaller one in left and right children
    if (child != currentSize && compare(array[child + 1], array[child]) < 0) {
      child++;
    }
    if (compare(array[child], temp) < 0) {
      // copy the smaller child up
      array[hole] = array[child];
    } else {
      break;
    }
  }
  array[hole] = temp;
}
```

##### The `buildHeap` Operation
+ The `buildHeap` operation can be done in **linear time** by applying a percolate down routine to nodes in reverse level order.
+ A constructor that accepts a collection containing an initial set of items and calls `buildHeap()`. (One `buildHeap` is more efficient than doing $N$ insertions.) The N successive insertion do more work than we require because they maintain heap order after every insertion and we need heap order only at one instant.

```java
private void buildHeap() {
  for (int i = currentSize / 2; i > 0; i--) {
    percolateDown(i);
  }
}
```

> **Theorem 21.1**
For the perfect binary tree of height $H$ containing $N = 2^{H+1} - 1$ nodes, the sum of the heights of the nodes is $N-H-1$.

##### `decreaseKey` and `merge`
Todo

##### Internal Sorting - Heapsort
1. Tossing each item into a binary heapsort (_Linear time_)
2. Appliying buildHeap (_Linear time_)
3. Calling `deleteMin` $N$ times, with the items exiting the heap in sorted order. (each call to `deleteMin` takes logarithmic time, so $N$ calls take $O(N \log N)$ time.)

###### Max Heap
For a typical increasing sorted order, we use a **max heap**, where the parent has a larger key than the child does.
1. For consistency with other sorting algorithm, sentinel position (0) is no longer used, and the data starts in position 0.

```java
// Standar heapsort
public static <AnyType extends Comparale<? super AnyType>> void heapsort(AnyType[] a) {
  // buildHeap
  for (int i = a.length / 2 - 1; i>= 0; i--) {
    percDown(a, i, a.length);
  }

  // deleteMax
  for (int i = a.length - 1; i > 0; i--) {
    swapReferences(a, 0, i);
    percDown(a, 0, i);
  }
}
```
