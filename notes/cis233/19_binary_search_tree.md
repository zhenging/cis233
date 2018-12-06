### 19 Binary Search Trees

#### Binary search tree order property
In a binary search tree, for every node $X$, all keys in $X$'s left subtree have smaller values than that key in $X$, and all keys in $X$'s right subtree have larger values than the key in $X$.

#### Operations

##### `find`, `findMin` and `findMax`
We can perform a `find` operation by starting at the root and then repeatedly branching either left or right, depending on the result of a comparison. `findMin` and `findMax`. The `findMin` operation is performed by following left nodes as long as there is a left child. The `findMax` operation is similar.

```java
private BinaryNode<AnyType> find(AnyType x, BinaryNode<AnyType> t) {
  while (t != null) {
    if (x.compareTo(t.element) < 0) {
      t = t.left;
    } else if (x.compareTo(t.element) > 0) {
      t = t.right;
    } else {
      return t; // Match
    }
  }
  return null; // Not Found
}

// Internal method to find the smallest item in a subtree
protected BinaryNode<AnyType> findMin(BinaryNode<AnyType> t) {
  if (t != null) {
    while (t.left != null) {
      t = t.left;
    }
  }

  return t;
}

// Internal method to find the largest item in a subtree
protected BinaryNode<AnyType> findMax(BinaryNode<AnyType> t) {
  if (t != null) {
    while (t.right != null) {
      t = t.right;
    }
  }

  return t;
}
```
1\. Test against `null` must be performed first, otherwise, the access `t.element` would be illegal.
2\. Because of call by values, the actual argument(root) is not changed. `t` is simply a _copy of root_.

##### Insertion
If the tree is empty, we can create a one-node tree, and return this newly created root node. If the tree is not empty, there are three possibilities. _First_, if the item to be inserted is smaller than the item in node `t`, we call `insert` recursively on the left subtree. _Second_, if the item is larger than the item in the node `t`, we call `insert` recursively on the right subtree. `Third`, if the item to insert matches the item in `t`, we throw  an exception.
```java
protected BinaryNode<AnyType> insert(AnyType x, BinaryNode<AnyType> t) {
  if (t == null) {
    return new BinaryNode<AnyType>(x);
  } else if (x.compareTo(t.element) < 0) {
    t.left = insert(x, t.left);
  } else if (x.compareTo(t.element) > 0) {
    t.right = insert(x, t.right);
  } else {
    throw new DuplicateItemException(x.toString()); // Duplicate
  }

  return t;
}

```

##### Deletion
`remove`. It's difficult to `remove` because nonleaf nodes hold the tree together and we do not disconnect the tree. For a node having two children, the general strategy is to replace the item in this node with the smallest item in the right substree (which is easily found) and then remove that node (which is now logically empty). The second `remove` is easy to do because, the minimum node in a tree does not have a left child.

#### Analysis of BST operations
The cost of an operation is proportional to the depth of the last accessed node. The cost is _logarithmic_ for a well-balanced tree, but it could be as bad as _linear_ for a degenerate tree.

#### AVL Tree
An AVL Tree is a binary search tree with the additional balance property that, for any node in the tree, the height of the left and right subtrees can differ by at most 1. As usual, the height of an empty subtree is $-1$.

An update in an AVL tree could destroy the balance. It must then be rebalanced before the operation can be considered complete.

1. An insertion in the left subtree of the left child of X.
2. An insertion in the left subtree of the right child of X.
3. An insertion in the right subtree of the left child of X.
4. An insertion in the right subtree of the right child of X.

##### Single Rotation
```java
// case 1
// Rotate binary tree node with left child
static BinaryNode rotateWithLeftChild(BinaryNode k2) {
  BinaryNode k1 = k2.left;
  k2.left = k1.right;
  k1.right = k2;
  return k1;
}

// case 2
// Rotate binary tree node with right child
static BinaryNode rotateWithRightChild(BinaryNode k1) {
  BinaryNode k2 = k1.right;
  k1.right = k2.left;
  k2.left = k1;
  return k2;
}
```

##### Double Rotation
```java
// case 3
// Double rotate binary tree node: first left child with its right child, then // node k3 with its new left child.
static BinaryNode doubleRotateWithLeftChild(BinaryNode k3) {
  k3.left = rotateWithRightChild(k3.left);
  return doubleRotateWithLeftChild(k3);
}

// case 4
// Double rotate binary tree node: first right child with its left child. then
// node k1 with its new right child
static BinaryNode doubleRotateWithLeftChild(BinaryNode k1) {
  k1.right = rotateWithLeftChild(k1.right);
  return doubleRotateWithRightChild(k1);
}
```
