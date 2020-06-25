---
layout: post
title: How to traverse Graph, DFS and BFS
comments: true
categories: [Data Structure]
tags: [Graph, C]
toc: true
---

# About Data Structure Graph Traversal DFS and BFS

## How to Traverse Graph

![CQ2](/public/images/3graph1.PNG)

### 1. Depth-First Search (DFS)

- Start with the root node and traverse depth first in the graph.
- Use `Stack` and `Recursion` to implement.
  - Stack is `LIFO`, Last In First Out
  - Stack can be seen as `vertical structure`, and vertical structure has a `depth`.
- Requires `less memory than BFS` because you don't have to store pointers of neighboring nodes.

  ![CQ2](/public/images/3graph8.PNG)

  ![CQ2](/public/images/3graph5.PNG)

  ![CQ2](/public/images/3graph9.PNG)

  ![CQ2](/public/images/3graph2.PNG)

### 2. Breath-First Search (BFS)

- Start with the root node and traverse witdh first in the graph.
- Use `Queue`.
  - Queue is `FIFO`, First In First Out
  - The queue can be seen as `horizontal structure`, and the horizontal structure has a `width`.
- Requires `more memory than DFS` because you have to store pointers of neighboring nodes.

  ![CQ2](/public/images/3graph7.PNG)

  ![CQ2](/public/images/3graph6.PNG)

  ![CQ2](/public/images/3graph10.PNG)

  ![CQ2](/public/images/3graph3.PNG)

#### Both DFS and BFS have pros and cons. Depending on the situation, you should choose between DFS and BFS.

### BFS

- Use when you need to search the shortest path.
- The node you are looking for is not far from the root node.
- It is necessary to traverse the parts of the graph.
- When there is a difference in depth on the graph.

### DFS

- Use to search the entire graph.
- The node you are looking for is far from the root node.
- It is recommended to use it when there is not much differencei in depth on the graph.

#

#### Implementation

DFS and BFS [GitHub](https://github.com/HyoSup0513/study/blob/master/Datastructure/Graph/Graph%20Traversal/GraphTraversal.c)
