# Midterm Cheatsheet

A quick-reference guide for common Computer Science topics.

---

## Table of Contents
1. [Big-O Complexity](#big-o-complexity)
2. [Data Structures](#data-structures)
3. [Sorting Algorithms](#sorting-algorithms)
4. [Graph Algorithms](#graph-algorithms)
5. [Trees](#trees)
6. [Dynamic Programming](#dynamic-programming)
7. [Bit Manipulation](#bit-manipulation)
8. [Common Recurrences (Master Theorem)](#master-theorem)

---

## Big-O Complexity

| Notation | Name | Example |
|---|---|---|
| O(1) | Constant | Array index access |
| O(log n) | Logarithmic | Binary search |
| O(n) | Linear | Linear search |
| O(n log n) | Linearithmic | Merge sort, heap sort |
| O(n²) | Quadratic | Bubble/insertion/selection sort |
| O(2ⁿ) | Exponential | Recursive fibonacci |
| O(n!) | Factorial | Permutations |

**Space vs. Time trade-off**: Using more memory (e.g., a hash table) often reduces time complexity.

---

## Data Structures

### Array
- Random access: **O(1)**
- Insert/delete at end: **O(1)** amortized (dynamic array)
- Insert/delete in middle: **O(n)**

### Linked List
| Operation | Singly | Doubly |
|---|---|---|
| Access by index | O(n) | O(n) |
| Insert/delete at head | O(1) | O(1) |
| Insert/delete at tail | O(n) | O(1) |
| Search | O(n) | O(n) |

### Stack (LIFO)
- Push / Pop / Peek: **O(1)**
- Use cases: DFS, balanced parentheses, undo operations

### Queue (FIFO)
- Enqueue / Dequeue: **O(1)**
- Use cases: BFS, task scheduling

### Hash Table
| Operation | Average | Worst |
|---|---|---|
| Insert | O(1) | O(n) |
| Delete | O(1) | O(n) |
| Search | O(1) | O(n) |

- Load factor = n / capacity; resize when load factor > 0.75 (typical)
- Collision resolution: **chaining** (linked lists) or **open addressing** (linear probing, quadratic probing, double hashing)

### Heap (Priority Queue)
| Operation | Time |
|---|---|
| Insert (push) | O(log n) |
| Remove min/max (pop) | O(log n) |
| Peek min/max | O(1) |
| Build heap | O(n) |

- Min-heap: parent ≤ children
- Max-heap: parent ≥ children
- 0-indexed array representation: left child = `2i+1`, right child = `2i+2`, parent = `(i-1)//2`

---

## Sorting Algorithms

| Algorithm | Best | Average | Worst | Space | Stable? |
|---|---|---|---|---|---|
| Bubble Sort | O(n) | O(n²) | O(n²) | O(1) | ✅ |
| Selection Sort | O(n²) | O(n²) | O(n²) | O(1) | ❌ |
| Insertion Sort | O(n) | O(n²) | O(n²) | O(1) | ✅ |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) | ✅ |
| Quick Sort | O(n log n) | O(n log n) | O(n²) | O(log n) | ❌ |
| Heap Sort | O(n log n) | O(n log n) | O(n log n) | O(1) | ❌ |
| Counting Sort | O(n+k) | O(n+k) | O(n+k) | O(k) | ✅ |
| Radix Sort | O(nk) | O(nk) | O(nk) | O(n+k) | ✅ |

**Key ideas:**
- **Merge sort**: divide & conquer, always O(n log n), extra O(n) space
- **Quick sort**: pivot partitioning; worst case O(n²) with bad pivot (e.g., already sorted + first element pivot)
- **Counting/Radix sort**: non-comparison based; beats O(n log n) lower bound when key range is limited

---

## Graph Algorithms

### Representations
| | Adjacency Matrix | Adjacency List |
|---|---|---|
| Space | O(V²) | O(V + E) |
| Edge lookup | O(1) | O(degree) |
| Best for | Dense graphs | Sparse graphs |

### BFS (Breadth-First Search)
- Uses a **queue**
- Time: **O(V + E)**
- Finds **shortest path** (unweighted)
- Visits nodes level by level

### DFS (Depth-First Search)
- Uses a **stack** (or recursion)
- Time: **O(V + E)**
- Detects cycles, topological sort, connected components

### Dijkstra's Algorithm
- Shortest path in weighted graph with **non-negative** weights
- Time: **O((V + E) log V)** with a min-heap
- Greedy: always relax the minimum-distance unvisited node

### Bellman-Ford
- Shortest path with **negative** weights (no negative cycles)
- Time: **O(V · E)**
- Detects negative cycles

### Floyd-Warshall
- All-pairs shortest path
- Time: **O(V³)**, Space: **O(V²)**

### Topological Sort
- Only on **Directed Acyclic Graphs (DAGs)**
- Kahn's algorithm (BFS-based with in-degree) or DFS post-order

### Minimum Spanning Tree
| Algorithm | Time | Best when |
|---|---|---|
| Kruskal's | O(E log E) | Sparse graphs |
| Prim's | O(E log V) | Dense graphs |

---

## Trees

### Binary Search Tree (BST)
| Operation | Average | Worst (unbalanced) |
|---|---|---|
| Search | O(log n) | O(n) |
| Insert | O(log n) | O(n) |
| Delete | O(log n) | O(n) |

**BST property**: left subtree < node < right subtree (all nodes)

### Tree Traversals
```
     1
    / \
   2   3
  / \
 4   5
```
| Traversal | Order | Result |
|---|---|---|
| Inorder (L, Root, R) | Sorted for BST | 4, 2, 5, 1, 3 |
| Preorder (Root, L, R) | Copy tree | 1, 2, 4, 5, 3 |
| Postorder (L, R, Root) | Delete tree | 4, 5, 2, 3, 1 |
| Level-order (BFS) | Level by level | 1, 2, 3, 4, 5 |

### Balanced BSTs (AVL / Red-Black)
- Guarantee **O(log n)** for all operations
- AVL: balance factor (height diff) ≤ 1 per node; uses rotations
- Red-Black: looser balance; faster inserts/deletes in practice

### Binary Heap vs BST
| Feature | Heap | BST |
|---|---|---|
| Find min/max | O(1) | O(log n) |
| Search arbitrary | O(n) | O(log n) |
| Insert | O(log n) | O(log n) |
| Build from n elements | O(n) | O(n log n) |

---

## Dynamic Programming

**Two conditions for DP**:
1. **Optimal substructure** – optimal solution is built from optimal sub-solutions
2. **Overlapping subproblems** – same sub-problems solved multiple times

**Approaches**:
- **Top-down (memoization)**: recursion + cache
- **Bottom-up (tabulation)**: iterative, fill table in dependency order

### Classic Problems
| Problem | Complexity |
|---|---|
| Fibonacci | O(n) time, O(1) space (optimized) |
| 0/1 Knapsack | O(n·W) |
| Longest Common Subsequence (LCS) | O(m·n) |
| Longest Increasing Subsequence (LIS) | O(n log n) with patience sort |
| Coin Change | O(n·amount) |
| Edit Distance | O(m·n) |
| Matrix Chain Multiplication | O(n³) |

### DP Template
```python
# Bottom-up example: Fibonacci
dp = [0] * (n + 1)
dp[0], dp[1] = 0, 1
for i in range(2, n + 1):
    dp[i] = dp[i-1] + dp[i-2]
return dp[n]
```

---

## Bit Manipulation

| Operation | Expression | Notes |
|---|---|---|
| Check bit k | `x & (1 << k)` | Non-zero if bit k is set |
| Set bit k | `x \| (1 << k)` | |
| Clear bit k | `x & ~(1 << k)` | |
| Toggle bit k | `x ^ (1 << k)` | |
| Clear lowest set bit | `x & (x - 1)` | Useful to count bits |
| Isolate lowest set bit | `x & (-x)` | |
| Check power of 2 | `x > 0 and (x & (x-1)) == 0` | |
| Count set bits | `bin(x).count('1')` or Brian Kernighan | |

---

## Master Theorem

For recurrences of the form **T(n) = a·T(n/b) + f(n)**  
where a ≥ 1, b > 1:

Let **c = log_b(a)**

| Case | Condition | Result |
|---|---|---|
| Case 1 | f(n) = O(n^(c−ε)) for some ε > 0 | T(n) = Θ(n^c) |
| Case 2 | f(n) = Θ(n^c · log^k n), k ≥ 0 | T(n) = Θ(n^c · log^(k+1) n) |
| Case 3 | f(n) = Ω(n^(c+ε)) and regularity holds | T(n) = Θ(f(n)) |

**Common examples**:
- Merge sort: T(n) = 2T(n/2) + O(n) → c = 1, f(n) = O(n) → Case 2 → **O(n log n)**
- Binary search: T(n) = T(n/2) + O(1) → c = 0, f(n) = O(1) → Case 2 → **O(log n)**
- Strassen's matrix multiply: T(n) = 7T(n/2) + O(n²) → c = log₂7 ≈ 2.81, Case 1 → **O(n^log₂7)**

---

## Quick Reference: Python Collections

```python
from collections import defaultdict, Counter, deque
import heapq

# Stack
stack = []
stack.append(x)   # push
stack.pop()       # pop

# Queue
q = deque()
q.append(x)       # enqueue
q.popleft()       # dequeue

# Min-heap
heap = []
heapq.heappush(heap, val)
heapq.heappop(heap)       # returns smallest
heapq.heapify(list)       # O(n) in-place

# Max-heap (negate values)
heapq.heappush(heap, -val)
-heapq.heappop(heap)

# Counter
c = Counter(iterable)
c.most_common(k)           # k most frequent

# Default dict
d = defaultdict(list)
d[key].append(val)         # no KeyError
```
