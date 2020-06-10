---
layout: post
title: What is a Tree ?
comments: true
categories: [Data Structure]
---

# Data Structure Tree

## What is a Tree ?

- A tree is a collection of node made up of hierarchical structures.
  - Parent-Child relationship
  - The next node can be multiple, but the previous node must be one.

## What is an Edge?

- A line that connects between nodes. The edge is used to indicate a parent-child relationship.

---

## Type of Node

Node that are distinguished by the position of nodes in the tree.

- Root node - First node in the tree
- Leaf node - node without a child node.
- Internal node - node with child node

Node that are distinguished by the relationship between nodes in the tree.

- Parent node - node connected directly above the child node
- Child node - node connected to the bottom of a node
- Ancestor node - all nodes in the path from the parent node to the root node
- Descendent node - all child nodes associated with one node
- Sibling node - node with the same parent node

![CQ2](/public/images/tree2.PNG)

### Root and Edge

![CQ2](/public/images/tree3.PNG)

### Internal node and Leaf node

![CQ2](/public/images/tree4.PNG)

### Parent, child and Sibling node

![CQ2](/public/images/tree5.PNG)

### Descendant and Ancestor node

![CQ2](/public/images/tree10.PNG)

---

## Term of Node

Terms of node

- Level - Distance from root node
- Height - The number of edges on the longest downward path between the root and a leaf
- Degree - Number of child nodes a node has

![CQ2](/public/images/tree6.PNG)

### Example of Level

1. Because A is the root node, Level 1
2. Because B and C are 1 distance from the root node, Level 2
3. Because D,E,F, and G are 2 distance from the root node, Level 3
4. Because H is 3 distance from the root node, Level 4

![CQ2](/public/images/tree7.PNG)

### Example of Height

1. Because H has no children, Height 1
2. Because E,F, and G also have no children, Height 1
3. Because D and C have 1 edge to the furthest node, Height 2
4. Because B has 2 edges to the furthest node H, Height 3
5. Because A has 3 edges to the furthest node H, Height 4

![CQ2](/public/images/tree8.PNG)

### Example of Degree

1. H,E,F, and G have no children, Degree is 0
2. D has one child H, Degree is 1.
3. B and C have 2 children, Degree is 2.
4. A has 2 children, Degree is 2.

![CQ2](/public/images/tree9.PNG)

---
