# Algorithm Evaluation

## Time Complexity

### Calculation
1. Consider only the worst case
2. Eliminate low order terms
3. Eliminate multiplicative constants

### $\varTheta$ Definition

$R(N) \in \varTheta(f(N))$ 

means there exist positive constants $k_1$ and $k_2$ such that:

$k_1 \cdot f(N) \le R(N) \le k_2 \cdot f(N)$

for all values of N greater than some $N_0$. (i.e. very large N)

### $O$ and ($\varOmega$)

$R(N) \in O(f(N))$ -> $ R(N) \le k_2 \cdot f(N)$
$R(N) \in \Omega(f(N))$ -> $ R(N) \le k_2 \cdot f(N)$

### Amortized Runtime

Any single operation may take longer, but if we use it over many operations, we're guranteed to have a better average performance.


# Data Structure

## Linked Data Structures

### Basic

1. IntNode (Basic Structure)

    ```java
    public class IntNode {

        public int item;
        public IntNode next;

        public IntNode(int f, IntNode r) {
            item = f;
            next = r;
        }
    }
    ```
2. Generics List

    - Using `Generics` to build list

### SLList 
(Singly Linked List)
[(Here is the code)](./Blocks/SLList.md)
   
```
(sentinel)
+--------+     +--------+     +--------+     +--------+
|   0    | --> |  item  | --> |  item  | --> |  item  | --> null
+--------+     +--------+     +--------+     +--------+
```
 - Promotions :
      - `size`
      - `sentinel`
  
### DLList 
(Doubly Linked List)
(Circular Sentinel)

```
    +--------+      +--------+      +--------+      +--------+
    |sentinel| <--> |  item  | <--> |  item  | <--> |  item  |
    +--------+      +--------+      +--------+      +--------+
        ^                                               ^
        |_______________________________________________|
```

- Promotions :
       - `last` (quicker access)

## Array (Java)

### Basic
1. Arrays are a special kind of object which consists of a **numbered** sequence of memory boxes.
2. Array's length cannot be changed.
3. Arrays do not have method.
4. Create a new array :
    ```java
    int[] x = new int[5];                   
    int[] y = new int[]{0, 1, 2, 95, 4};
    int[] z = {0, 1, 2, 3, 4};
    ```
5. Arrays have an attribute `length`.
6. Copy arrays
    ```java
    System.arraycopy(a, 0, b, 2, 3); //Java
    ```
    ```python 
    b[2:5] = a[0:3] "Python"
    ```

### AList
(Resizing Array)
[(Here is the code)](./Blocks/AList.md)

## Stack

### Definition

First in, last out

Main operations:
- `push`: addFirst
- `pop`: removeFirst 

## Queue

### Definition

First in, first out

Main opreations:
- `enqueue`: addLast
- `dequeue`: removeFirst


## Set

### Definition

A Set is a collection of unique items.

Main operations:
- `add(x)`: add item x
- `contains(x)`: check whether x exists
- `remove(x)`: remove x
- `size()`: return the number of items

### Key Properties

- No duplicate items.
- Usually only stores keys, not values.
- Common implementations:
  - BSTSet
  - HashSet
  - TreeSet

### Set vs List

- List cares about order and index.
- Set cares about membership: whether an item exists.

## Map

### Definition

A Map stores key-value pairs.

Main operations:
- `put(key, value)`: insert or update a key-value pair
- `get(key)`: get the value associated with the key
- `containsKey(key)`: check whether the key exists
- `remove(key)`: remove the key-value pair
- `size()`: return the number of pairs

### Key Properties

- Keys are unique.
- Values can be duplicated.
- Each key maps to exactly one value.
- Common implementations:
  - BSTMap
  - HashMap
  - TreeMap

## Disjoint Sets (并查集)

### Basic
The Disjoint Sets data structure has two operations:
- connect(x, y): Connects x and y
- isConnected(x, y): Returns true if x and y are connected. Connections can be transitive, i.e. they don't need to be direct.

```java
public interface DisjointSets {
    /** Connects teo items P and Q.*/
    void connect(int p, int q);

    /** Checks to see if two items are connected. */
    boolean isConnected(int p, int q);
}
```

### Asymptotics
1. ListOfSetsDS
    List of sets. 

    | Constructor | connect | isConnected |
    | --- | --- | --- |
    |$$\varTheta(N)$$ | $$O(N)$$ | $$O(N)$$ |


2. QuickFindDS
    List of integers where ith entry gives set number(a.k.a. "id") of item i.

    [Here is the code](./Blocks/QuickFindDS.md)
    | Constructor | connect | isConnected |
    | --- | --- | --- |
    | $$\varTheta(N)$$ |  $$\varTheta(N)$$ |  $$\varTheta(1)$$ |

3. QuickUnionDS
    Trees of connected items.
    - In the parent array, each index represents an item, and the value at that index represents that item's parent.
    - The root-item's value in the parent array is `-1`.

    [Here is the code](./Blocks/QuickUnionDS.md) 
    | Constructor | connect | isConnected |
    | --- | --- | --- |
    | $$\varTheta(N)$$ | $$O(N)$$ | $$O(N)$$ |

    (Trees can get very tall, so isConnected is O(N))

4. WeightedQuickUnionDS
    The improvement of QuickUnionDS, avoiding too tall tree.
    - In the parent array, each index represents an item, and the value at that index represents that item's parent.
    - The rule to merge two trees is based on weight, not height. (Simply because the weighted QuickUnion is easier to code, and both of them are $O(\log N)$)
    - The root stores the `negative size`(weight) of its tree in the parent array.

    | Constructor | connect | isConnected |
    | --- | --- | --- |
    | $$\varTheta(N)$$ | $$O(\log N)$$ | $$O(\log N)$$ |

### Completion

**Weighted QuickUnion with Path Compression**

The improvement of WeightedQuickUnionDS, using path compression.
- During find, perform `path compression` by making every node on the path point directly to the root. (Recursively)

[Here is the code](./Blocks/WeightedQuickUnionWithPathCompression.md)
| Constructor | connect | isConnected |
| --- | --- | --- |
| $$\varTheta(N)$$ | $$O(\alpha(N))$$ | $$O(\alpha(N))$$ |

(where α(N) is the inverse Ackermann function, which grows so slowly that for any practical N, it is less than 5.)

**Weighted Quick Union with Path Compression has almost constant time operations.**

## Priority Queue

### Definition

A Priority Queue is an ADT that supports adding items and quickly accessing/removing the item with the highest priority.

In CS61B Lecture 21, we mainly discuss the **Min Priority Queue**, where the most important item is the smallest item.

Main operations:
- `add(x)`: adds item x to the priority queue
- `getSmallest()`: returns the smallest item
- `removeSmallest()`: removes and returns the smallest item
- `size()`: returns the number of items

### Priority Queue vs Heap

- **Priority Queue** is an ADT: it describes what operations we want.
- **Binary Min-Heap** is a concrete data structure: it describes how we implement the Priority Queue efficiently.

### Completion

Using **Binary Min-Heap**


| add | getSmallest | removeSmallest |
| --- | --- | --- |
| $$\varTheta(\log N)$$ | $$O(1)$$ | $$\varTheta(\log N)$$ |




# Trees

## Definition
1. Trees
   - A set of nodes.
   - A set of edges that connect those nodes.
     - Constraint: There is exactly one path between any two nodes.

2. Rooted Tree
   - In a rooted tree, we call one noede the root.
   - Every node N except the root has exactyly one parent, defined as the first node on the path from N to the root.
   - The root is usually depicted at the top of the tree.
   - A node with no child is called a leaf.

3. Rooted Binary Tree
   - Every node has either 0, 1 or 2 children (subtrees).

## Representations

### Explicit Child References

Each node directly stores references to its children.

#### Fixed-Width Nodes

```java
public class Tree1A<Key> {
    Key key;
    Tree1A<Key> left;
    Tree1A<Key> middle;
    Tree1A<Key> right;
}
```

#### Variable-Width Nodes

```java
public class Tree1B<Key> {
    Key key;
    Tree1B<Key>[] children;
}
```

#### First-Child Next-Sibling Representation

```java
public class Tree1C<Key> {
    Key key;
    Tree1C<Key> firstChild;
    Tree1C<Key> nextSibling;
}
```

### Array with Parent Links

```java
public class Tree2<Key> {
    Key[] keys;
    int[] parents;
}
```

### Array Representation for Complete Trees

For complete trees, store nodes in level order in an array.

This is used for Binary Heaps.

Usually index 0 is left empty.

Example:
```
Index:  1  2  3  4  5  6  7
Array: [A, B, C, D, E, F, G]
```
```
        A
      /   \
     B     C
    / \   / \
   D   E F   G
```

```java
leftChild(k) = 2 * k;
rightChild(k) = 2 * k + 1;
parent(k) = k / 2;
``` 

## Traversal

```
        A
      /   \
     B     C
    / \   / \
   D   E F   G
```
**Depth First Traversals**
- `Level Order`: ABCDEFG

**Depth First Traversals**
- `Preorder`: ABDECFG
- `Inorder`: DBEAFCG
- `Postorder`: DEBFGCA

### Visual Trick

For humans, we trace a path around the graph, from the top going counter-clockwise.

**Preorder**: "Visit" when you cross the left of a node
**Inorder**: "Visit" when you cross the bottom of a node
**Postorder**: "Visit" when you cross the right of a node



## Binary Search Trees (BST)

### Definition
A binary search tree is a rooted binary tree with the BST property.

**BST Property**. For evety node X in the Tree:
- Every key in the `left` subtree is `less` than X's key.
- Every key in the `right` subtree is `greater` than the X's key.

Ordering must be complete, transitive, and antisymmetric

No duplicate keys allowed.

### Asymptotics

1. BST invariant
    - left < node < right
 
2. find / get
    - compare and go left / right

3. insert / put
    - Same travarsal as find
    - Create node at null

4. delete
    - 0 child -> return null
    - 1 child -> return child
    - 2 child 

**Deletion with two Children (Hibbard)**
- Find the leftmost node in the right subtree.
- Replace the deleted node’s key with this successor’s key.
- Then delete the successor node from the right subtree.

### Completion
[Here is the code](./Blocks/BSTmap.md)

| find | insert | delete |
|---|---|---|
|$$O(h)$$|$$O(h)$$|$$O(h)$$|

- worst case: $\varTheta(N)$ (skewed tree)
- balanced: $\varTheta(log N)$

## Tree Rotation

### Definition
Tree rotation is a local restructuring operation that:
- changes the shape of a tree
- preserves the BST property 

Example - rotateRight(P)
```

        p                       G - P                       G
       / \                     /  |  \                     / \ 
      G   R                   C   K   R                   C   P
     / \            ->       /   / \           ->        /   / \
    C   K                   A   J   L                   A   K   R
   /   / \                                                 / \
  A   J   L                                               J   L

```
Using rotation to balance a tree paying $O(N)$ time.

## B-Trees

### Definition

A B-Tree is a balanced multi-way search tree.
- Each node can hava multiple keys + multiple children.
- Designed to keep the tree shallow.
  

**Node structure**
We call a node `x-node` with x children 
```
    [ key1 | key2 | key3 | ... ]
    /      |      |      |     \
 child   child  child  child  child
 ```
 - Keys are sorted.
 - Children split ranges:
   - left subtree < key1
   - betweern key1 & key2
   - ...
   - right subtree > last key

**Invariants**
Operations = $O(\log N)$
All leaves must be the same distance from the root.
A non-leaf node with k items must have exactly k+1 item.

### 2-3 Tree (L = 2)

A node can have 1-2 keys and 0-3 subtrees

1. search 
   - Same idea as BST, just more branches

2. insert
    - case 1: insert into a 2-node (directly)
    - case 2: insert into a 3-node (overflow) -> split

**Split Rule**
- middle key goes up
- others become children

### 2-3-4 Tree (L = 3)

A node can have 1-3 keys and 0-4 subtrees

## Left Leaning Red-Black Trees (LLRBs)

### Definition
A Left-Leaning Red-Black Tree (LLRB) is a binary search tree that simulates a 2-3 tree using red links, where all red links lean left.

### Asymptotics
- When inserting: Use a red link.
- If there is a *right leaning "3-node"*, we have a **Left Leaning Violation**.
  - Rotate left the appropriate node to fix.
- If ther are two *consecutive left links*. we have a **Incorrect 4-Node Violation**.
  - Rotate right the appropriate node to fix.
- If there are any *nodes with two red children*, we have a **Temporary 4-Node**.
  - Color flip the node to emulate the split operation.

- Pay attention to `Cascading Balance`.(连锁反应)

### Property

**An LLRB has no more than ~2x the height of its 2-3 tree.**

**All the case**
- 右红左黑 → 左旋
- 左左连续红 → 右旋
- 左右都红 → 颜色翻转

### Completion

[Here is the code](./Blocks/LLRB.md)

# Hashing

## Definition

### Hash tables
- Data is converted into a hash code, the hash code is then reduced to a valid index.
- Data is then sorted in a bucket corresponding to that index.
  - Each bucket is a "separate chain" of items
- Resize when load factor N/M exceeds some constant.
  
### Require
- Don't **Mutate** Keys

# Graph

## Definition

A simple graph:
- No edges that connect a vertex to itself
- No two edges that connect the same vertices

Types: Directed/Undirected, Acyclic/Cyclic, With Edge Labels

**Terminology**
- Graph
  - Set of *vertices*, a.k.a. *nodes*
  - Set of *edges*
  - Vertices with an edge between are *adjacent*
  - Vertices or edges may have *labels* (or *weights*)
- Path
  - A sequence of vertices connected by edges
  - A *simple path* is a path without repeated vertices
- Cycle
- Connected
- Degree 
  - = # edges

## Representations

### API
```java
public class Graph {
    public Graph(int V):                // Create empty graph with v vertices
    public void addEdge(int v, int w):  // add an edge v-w
    Iterable<Integer> adj(int v):       // vertices adjacent to v
    int V():                            // number of vertices
    int E():                            // number of edges
}
```

### Adjacency Matrix

### Adjacency List

## Traversal

### DFS

RunTime O(V + E)

**DFS Preorder**: Action is before DFS calls to neighbors

**DFS Postorder**: Action is after DFS calls to neighbors

### BFS 

- Initialize a queue with a starting vertex s anmd mark the vertex
- Repeat until queue is empty:
  - Remove vertex v from the front of the queue
  - For each unmarked neighbor n of v
    - Mark n
    - Set edgeTo[n] = v (and distTo[n] = distTo[v] + 1)
    - Add n to end of queue

## Shortest Paths

*The graph has no negative weight edges.*
*The graph is Directed/Undirected.*
*We choose a starting vertex.*

### Dijkstra's Algorithm

Dijkstra repeatedly finalizes the closest unmarked vertex.

1. Initialize:
   - `distTo[source] = 0`
   - all other distances = infinity
   - PQ ordered by `distTo`

2. Repeat:
   - Remove the closest unmarked vertex `v` from the PQ.
   - Mark `v`.
   - Relax all outgoing edges `v -> w` where `w` is unmarked.

3. Relaxation:
   - If going through `v` gives a shorter path to `w`, update `distTo[w]`, `edgeTo[w]`, and PQ priority.

**Run Time** 

$O(E \log V)$ for a connected graph.

### A* Algorithm

A* is like Dijkstra's algorithm, but the priority is `distTo[v] + heuristic(v, goal)`(distance + penalty), so it prefers vertices that are both cheap to reach and estimated to be closer to the goal.

## Minimum Spanning Trees

*Negative weight edges are allowed.*
*The graph is Undirected.*
*We do not choose a starting vertex.*

### Definition

**Spanning Tree**
- a subgraph of an undirected graph, where it:
  - is connected
  - is acyclic
  - includes all of the vertices

A **minimum spanning tree** is a spanning tree of minimum total weight.

### Prim's Algorithm

**Basic Prim's**
Start from some arbitrary start node.
- Repeatedly add shortest edge that has one node inside the MST under construction.
- Repeat until V - 1 edges.

**Optimized Prim's**
- Insert all vertices into fringe PQ, storing vertices in order of `distance from tree`. 
- Repeat: Remove (closest) vertex v from PQ, and relax all edges pointing from v.

**Run Time** 
$O(E \log V)$ for a connected graph.

### Kruskal's Algorithm

- Consider edges in order of increasing weight. (Using `PQ`)
- Add to MST unless a cycle is created. (Using `Disjoint Set`)
- Repeat until V - 1 edges

**Run Time**
$O(E \log E)$ for a connected graph.

## Directed Acyclic Graphs

### Topological ordering
- When nodes are sorted in diagram, arrows all point rightwards.

**Topological sort**
Perform a DFS traversal from every vertex eith indegree 0, NOT clearing markings in between traverals.
- Record DFS postorder in a list.
- Topological ordering is givern by the reverse of that list (reverse postorder).

**Run Time**
$O(V + E)$

### DAG SPT Algorithm
The Shortest Paths Problem on DAGs.

Visit vertices in topological order.
- When we vist a vertex: relax all of its going edges.

**Run Time**
$O(V + E)$

### DAG LPT Algorithm
The Longest Paths Problem on DAGs.

DAG LPT solution for graph G:
- Form a new copy of the graph G' with signs of all edge weights flipped.
- Run DAGSPT on G' yielding result X.
- Flip signs of all values in X.distTo.
- X.edgeTo is already correct.

**Run Time**
$O(V + E)$

# Trie

## Definition
Short for Retrieval Tree.

For String keys:
- Every node stores only one letter.
- Nodes can be shared by multiple keys.
- Mark at the end of the key.

## Operations

The main appeal of tries is their ability to efficiently support string specific operations like prefix matching.