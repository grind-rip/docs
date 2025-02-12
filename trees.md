# Trees

A tree is a hierarchical data structure that consists of nodes connected by edges. Each node in a tree can be connected to one or more child nodes (depending on the type of tree) or no nodes if it is a leaf node. Each node can be connected to exactly one parent—except for the root node, which has no parent.

A tree is an undirected, connected, acyclic graph. This means there are no cycles or "loops" (no node can be its own ancestor), and also that each child can be treated like the root node of its own subtree, making recursion a useful technique for tree traversal. The acyclic nature of a tree is an important characteristic, because unlike with general graphs (which may have cycles), keeping track of "visited" nodes is not necessary.

## Terminology

* **Node**: A structure that may contain data and references (edges/links) to other nodes.
* **Parent Node**: A node that has one or more child nodes.
* **Child Node**: A node connected to a parent node. Each child has exactly one parent node.
* **Sibling Node**: A node with the same parent as another child node.
* **Ancestor Node**: A node reachable by repeatedly moving from child to parent.
* **Descendant Node**: A node reachable by repeatedly moving from parent to child.
* **Root Node**: The topmost node in a tree. Every tree has exactly one root.
* **Leaf Node**: A node that has no child nodes.
* **Internal Node**: Any node in a tree that has child nodes.
* **External Node**: Any node in a tree that does not have child nodes. Also known as a leaf node.
* **Neighbor Node**: Two nodes are considered neighbors if they are directly connected to each other by an edge.
* **Node Depth**: The number of edges on the unique path from the root to the node. A tree with only one node (i.e., both root and leaf) has depth and height zero.
* **Node Height**: The number of edges along the unique path from the node to a leaf. The height of the root is the height of the tree.
* **Degree**: The degree of a node is the number of its child nodes. The degree of a tree is the maximum degree of all the nodes in the tree.
* **Distance**: The number of edges along the shortest path between two nodes.
* **Level**: The level of a node is the number of edges along the unique path between it and the root node. This is the same as depth.
* **Width**: The maximum number of nodes at any one level in the tree.
* **Breadth**: Same as width.
* **Ordered Tree**: A tree in which an ordering is specified for the child nodes of a parent.
* **Size**: The number of nodes in the tree.

```
         A          [A]                      = Root node
         ●          [A, B, C]                = Parent nodes
       /   \        [B, C, D, E, F, G]       = Child nodes
     B       C      [D, E, F, G]             = Leaf nodes
     ●       ●      [[B, C], [D, E], [F, G]] = Sibling nodes
   /   \   /   \
  D     E F     G
  ●     ● ●     ●   Depth = 2, Breadth = 4, Degree = 2, Size = 7
```

## Tree Traversal

Tree traversal is the process of visiting each node in a tree exactly once. Such traversals are classified by the order in which the nodes are visited. There are two main tree traversals: depth-first and breadth-first search. Additionally, depth-first search can be done pre-order, post-order, and in-order.

**Depth-first search**
Depth-first search explores a branch of the tree as deeply as possible before backtracking and moving on to the next branch. Depth-first search can be implemented iteratively using a stack or recursively, in which case the stack is implicit via the call stack. No single traversal order (pre-order, post-order, or in-order) uniquely identifies the structure of a tree. Therefore, to uniquely serialize a tree, you generally need two traversals (for example, pre-order and in-order, or post-order and in-order).

**Pre-order**

```
A → B → D → E → C → F → G
```

1. Visit the current node.
2. Recursively traverse the current node's left subtree.
3. Recursively traverse the current node's right subtree.

Pre-order traversal produces an ordering where each parent appears before its children—this property resembles a topological ordering in graphs.

**Post-order**

```
D → E → B → F → G → C → A
```

1. Recursively traverse the current node's left subtree.
2. Recursively traverse the current node's right subtree.
3. Visit the current node.

Post-order traversal can be useful for obtaining the postfix expression of a binary expression tree.

**In-order**

```
D → B → E → A → F → C → G
```

1. Recursively traverse the current node's left subtree.
2. Visit the current node.
3. Recursively traverse the current node's right subtree.

In-order traversal is very commonly used on binary search trees because it returns values from the underlying set in order, according to the comparator that set up the binary search tree.

**NOTE**: Pre-, post-, and in-order traversals can all be done in reverse as well.

**Breadth-first search**
With breadth-first search (sometimes called level-order traversal), each node at a given depth (or level) is visited before moving on to the next level. Breadth-first search is typically implemented iteratively using a queue.

```
A → B → C → D → E → F → G
```

## Binary Trees

A binary tree is a tree data structure in which each node has at most two children, referred to as the left child and the right child. Binary trees are the most common tree structure.

### Terminology

* **Complete binary tree**: A binary tree in which every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. That is, all internal nodes have two children and all external (leaf) nodes have no children.
* **Balanced binary tree**: A binary tree in which the left and right subtrees of every node differ in height by no more than 1.

## Binary Search Tree (BST)

A binary search tree (BST) is a binary tree in which the key of each internal node is greater than all the keys in the node's left subtree and less than all the keys in the node's right subtree. A property of a binary search tree is that an in-order traversal will yield all the nodes in ascending order.

## Time Complexity

| Operation | Big O    |
| --------- | -------- |
| Access    | O(log n) |
| Search    | O(log n) |
| Insert    | O(log n) |
| Delete    | O(log n) |

**NOTE**: Logarithm time complexity holds only for balanced binary search trees. For an unbalanced BST, operations can degrade to O(n).

## Common Operations

* Enumerating all nodes in the tree.
* Enumerating all nodes in a subtree of the tree.
* Searching for a node.
* Calculating the height of the tree.
* Adding a new node at a specific position in the tree.
* Inserting a node.
* Deleting a node.
* Pruning (i.e., removing a subtree from the tree).
* Grafting (i.e., adding a subtree to the tree).
* Finding the root from a node.
* Finding the lowest common ancestor of two nodes.

For binary search trees:
* Validate binary search tree.
* Get max node.
* Get min node.

## Augmented Trees

An augmented data structure stores additional information in each of its nodes that would otherwise be expensive to compute. For trees, this might include information like the size of a subtree (which can be useful for ranking values, where we want to determine how many elements of the tree are smaller), the height of a subtree, or other summary information like the sum of all the keys in a subtree.

Augmented data structures violate a general programming principle that states the same information should not be stored in different places, since maintaining state is complex and error prone. However, given the benefit gained through augmentation, the complexity cost is justified.

Additionally, since tree operations only modify the nodes on the path from the root to the impacted node and computation can be done in constant time from precomputed values, the total cost of modifying nodes after a tree operation is O(log n) assuming the tree is balanced.

Augmented trees are used in AVL trees, ranking (order statistics), and range queries with O(log n) time complexity.

## Techniques

### Recursion

Given the properties of a tree - each child can be treated like the root node of its own subtree - recursion can be used to solve most problems. Pretty much every divide and conquer algorithm for binary trees looks like this:

```python
def do_something_to_all_nodes(root):
    """
    The canonical binary tree algorithm. Processes all nodes using pre-order
    traversal. Moving the call to `do_something()` between or after the two
    recursive calls yields an in-order or post-order traversal, respectively.
    """
    if root:
        do_something(root)                     # Process current node
        do_something_to_all_nodes(root.left)   # Process left subtree
        do_something_to_all_nodes(root.right)  # Process right subtree
```

### Tree Traversal

Tree traversal is a common operation. There are two main tree traversals: depth-first and breadth-first search. Additionally, depth-first search can be done pre-order, post-order, and in-order. Depth-first search can also be implemented iteratively using a stack.
