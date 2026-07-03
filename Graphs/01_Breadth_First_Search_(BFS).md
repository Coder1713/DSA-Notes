# Breadth First Search (BFS)

## Motivation

Suppose you need to find the minimum number of roads required to travel from one city to another.

The most logical approach is to first explore every city that is one road away, then every city that is two roads away, followed by every city that is three roads away.

Breadth First Search (BFS) follows exactly this strategy. Instead of exploring one path completely, it explores the graph level by level.

This property makes BFS the standard algorithm for shortest path problems in **unweighted graphs**.

---

## Intuition

Consider the following graph.

```
        A
      /   \
     B     C
    / \   / \
   D   E F   G
```

Starting from **A**, BFS visits the graph in the following order:

```
Level 0 : A

Level 1 : B C

Level 2 : D E F G
```

Every node at distance **k** from the source is visited before any node at distance **k + 1**.

The algorithm achieves this behaviour by using a **queue**, which processes nodes in the same order they are discovered.

---

## Pattern Recognition

BFS is usually the correct choice when a problem contains phrases such as:

- Shortest path in an unweighted graph
- Minimum number of moves
- Minimum number of operations
- Level order traversal
- Spread of infection or fire
- Multi-source expansion
- Reach every possible state

Whenever every edge has the same cost, BFS should be one of the first algorithms you consider.

---

## Core Idea

Maintain a queue containing nodes that have been discovered but not yet processed.

1. Insert the source node into the queue.
2. Mark it as visited.
3. Repeatedly remove the front node.
4. Visit each unvisited neighbour.
5. Mark every neighbour as visited before inserting it into the queue.

This guarantees that nodes are processed level by level.

---

## Algorithm

1. Create an empty queue.
2. Mark the source node as visited.
3. Push the source node into the queue.
4. While the queue is not empty:
   - Remove the front node.
   - Traverse all of its neighbours.
   - If a neighbour has not been visited:
     - Mark it as visited.
     - Push it into the queue.

---

## Why is a Queue Used?

A queue follows the **First In, First Out (FIFO)** principle.

Nodes discovered earlier belong to the current level and are therefore processed before nodes discovered later.

Replacing the queue with a stack would change the traversal into Depth First Search (DFS).

---

## Why Do We Mark a Node as Visited Before Pushing It?

Consider the graph:

```
A ----\
       X
B ----/
```

If `X` is marked as visited **after** it is pushed into the queue, both `A` and `B` may insert `X`.

```
Queue

X
X
```

The same node will now be processed twice.

Marking a node as visited **before** inserting it prevents duplicate entries.

---

## Dry Run

Graph:

```
0 → 1
|
2

1 → 3

2 → 4
```

Initial Queue

```
[0]
```

Process `0`

```
Queue : [1, 2]
```

Process `1`

```
Queue : [2, 3]
```

Process `2`

```
Queue : [3, 4]
```

Process `3`

```
Queue : [4]
```

Process `4`

```
Queue : []
```

Traversal Order

```
0 → 1 → 2 → 3 → 4
```

---

## Python Template

```python
from collections import deque

def bfs(start, graph):

    visited = {start}
    q = deque([start])

    while q:

        node = q.popleft()

        for neighbour in graph[node]:

            if neighbour not in visited:

                visited.add(neighbour)
                q.append(neighbour)
```

---

## Complexity Analysis

| Operation | Complexity |
|-----------|------------|
| Time | O(V + E) |
| Space | O(V) |

where

- `V` = Number of vertices
- `E` = Number of edges

---

## Common Mistakes

- Using a stack instead of a queue.
- Marking a node as visited after removing it from the queue.
- Forgetting the visited array, resulting in repeated processing.
- Assuming BFS always gives the shortest path, even for weighted graphs.
- Ignoring disconnected components.

---

## Variations

- Grid BFS
- Multi-source BFS
- 0-1 BFS
- Kahn's Algorithm
- Shortest Path in an Unweighted Graph

---

## Practice Problems

Easy

- Binary Tree Level Order Traversal
- Flood Fill

Medium

- Number of Islands
- Rotting Oranges
- Open the Lock
- Word Ladder
- Course Schedule

Hard

- Shortest Path Visiting All Nodes

---

## Key Takeaways

- BFS explores a graph level by level.
- A queue is responsible for maintaining level order traversal.
- BFS guarantees the shortest path only when all edge weights are equal.
- Always mark a node as visited before inserting it into the queue.
- The time complexity of BFS is `O(V + E)`.
