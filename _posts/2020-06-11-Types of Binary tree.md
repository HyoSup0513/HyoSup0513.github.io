---
layout: post
title: Types of Binary Tree
comments: true
categories: [Data Structure]
tags: [Tree]
---

# About Types of Binary Tree

## What is a Binary Tree ?

- A tree in which each node can have up to two child nodes.
- A tool for sorting and seraching algorithms.
  - Depending on the shape of the binary tree, the performance of the algorithm varies.
  - The shape of the tree depends on the level and number of nodes.

---

## Types of Binary Tree

### 1. Perfect Binary Tree

1. A full binary tree is a tree full of nodes at all levels.
   - Node has 2 children.
   - Degree is 2.
2. All nodes are full, so the height from the leaf node to the root node is the same.
3. Number of nodes n = 2^height - 1

![CQ2](/public/images/2tree1-mod.PNG)

A is full with B and C as children, and B is full with D and E, and C is full with F and G, so all levels are full.
Therefore, this tree is a Perfect binary tree.

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

---

### 4. Full Binary Tree

1. A full binary tree is a tree in which all nodes have only 0 or 2 child nodes.
2. 2 \* height + 1 <= Number of nodes n <= 2^(height+1) -1

![CQ2](/public/images/2tree4.PNG)

A has two child nodes B and C, B has two child nodes D and E, and C has no child node. So, this is a full binary tree.

---

### 5. Balanced Binary Tree

1. A balanced binary tree is a tree in which height of the left and right sub-trees of all nodes does not differ by more than 1.

![CQ2](/public/images/2tree7.PNG)

The trees on the left can be seen that the height of the sub-trees on the left and right are not more than 1 difference.

However, the trees on the right are not balanced because the height of the sub-trees on the left and right are more than 1 difference.
