---
layout: post
title: Tree Traversals (Inorder, Preorder, Postorder, Levelorder)
comments: true
categories: [Data Structure]
---

# About Types of Tree Traversals

## What is Tree Traversals ?

- Tree traversal is visiting every node of the tree once.
- The method of tree traversal depends on the order in which the nodes are visited.

---

## Terms for Tree Traversal

- V - Vist node
- L - Traverse the left subtree
- R - Traverse the right subtree

![CQ2](/public/images/3tree1mod.PNG)

---

## Types of Tree Traversals

### 1. Pre-order

1. Visit the node
2. Traverse the left subtree
3. Traverse the right subtree

![CQ2](/public/images/3tree2mod.PNG)

Visit node A

Traverse the left subtree of node A -> Visit node B

Traverse the the left subtree of node B -> Visit node D

Node D is a leaf node -> Return to node B -> Traverse the right subtree of node B -> Visit node E

Node E is a leaft node -> Return to node A -> Traverse the left subtree of node A -> Visit node C

Traverse the left subtree of node C -> Visit node F

Node F is a leaf node -> Return to node C -> Traverse the right subtree of node C -> Visit node G

Node G is the last node, finished visiting every node.

Therefore, A->B->D->E->C->F->G

---

### 2. In-order

1. Traverse the left subtree
2. Visit the node
3. Traverse the right subtree

![CQ2](/public/images/3tree3mod.PNG)

Traverse the left subtree of node A -> Move to node B -> Traverse the left subtree of node B -> Visit node D

Node D is a leaft node -> Return to node B -> Visiting node B's left subtree is finished, visit node B.

Traverse the right subtree of node B -> Visit node E

Node E is a leaf node-> Move to node B -> Move to node A, visiting node A's left subtree is finished -> Visit node A

Traverse the right subtree of node A -> Move to node C -> Traverse the left subtree of node C -> Visit node F

Node F is a leaf node -> Return to node C -> Visiting node C's left subtree is finished -> Visit node C

Traverse the right subtree of node C -> Visit node G

Node G is the last node, visiting every node is finished.

Therefore, D->B->E->A->F->C->G

---

### 3. Post-order

1. Traverse the left subtree
2. Traverse the right subtree
3. Visit the node

![CQ2](/public/images/3tree4mod.PNG)

Traverse the left subtree of node A -> Move to node B -> Traverse the left subtree of node B -> Visit node D

Node D is a leaf node -> Return to node B -> Traverse the right subtree of node B -> Visit node E

Node E is a leaft node -> Return to node B -> Visit node B

Visiting node B's subtree is finished, return to node A -> Traverse the right subtree of node A -> Move to node C ->
Traverse the left subtree of node C -> Visit node F

Node F is a leaf node -> Return to node C -> Traverse the right subtree of node C -> Visit node G

Node G is a leaft node -> Return to node C -> Visit node C

Visiting node C's subtree is finished, return to node A -> Visit node A

Node A is the last node, visiting every node is finished.

Therefore, D->E->B->F->G->C->A

---

### 4. Level-order aka Breadth-first traversal

1. Traverse the nodes in order from the lower level.

![CQ2](/public/images/3tree5mod.PNG)

Visit node A at the lowest level 1

Visit node B and C of level 2.

Vist node D, E, F, and G of level 3.

Node G is the last node.

Therefore, A->B->C->D->E->F->G
