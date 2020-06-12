---
layout: post
title: Types of Binary Tree
comments: true
categories: [Data Structure]
---

# About Types of Binary Tree

## What is a Binary Tree ?

- A tree in which each node can have up to two child nodes.
- A tool for sorting and seraching algorithms.
  - Depending on the shape of the binary tree, the performance of the algorithm varies.
  - The shape of the tree depends on the level and number of nodes.

---

## Types of Binary Tree

### 1. Full Binary Tree

1. A full binary tree is a tree full of nodes at all levels.
   - Node has 2 children.
   - Degree is 2.
2. All nodes are full, so the height from the leaf node to the root node is the same.
3. Number of nodes n = 2^height - 1

![CQ2](/public/images/2tree1.PNG)

A is full with B and C as children, and B is full with D and E, and C is full with F and G, so all levels are full.
Therefore, this tree is a full binary tree.

---

### 2. Complete Binary Tree

1. A complete binary tree is filled until just before the last level and then filled from left to left at the last level.
2. The concept of a full binary tree is related to heap.
3. Number of nodes n < 2^height - 1

![CQ2](/public/images/2tree2.PNG)

The tree on the left is a complete binary tree because it is filled with nodes from the left, but the tree on the right is not a complete binary tree because it is not filled from the left at level 3.

---

### 3. Skewed Binary Tree

1. A skewed binary tree is a tree that is skewed to the left or right.
2. There is only one node at each height.
   - Therefore, it is skewed only to the left or right.
3. height <= Number of nodes n <= 2^height - 1
   - The number of nodes in the skewed binary tree equals to height that is the minimum value in the expression above.
   - The maximum value is equal to the full binary tree's number of nodes.

![CQ2](/public/images/2tree3.PNG)

In the tree on the left, A has B as the left child, B has D as the left child, so it is the left skewed binary tree.
In the tree on the right, A has B as the right child, B has D as the right child, so it is the right skewed binary tree.
