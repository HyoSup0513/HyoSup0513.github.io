---
layout: post
title: Doubly Linked List Implementation 이중 연결 리스트 구현
comments: true
categories: [Data Structure]
tags: [Doubly Linked List]
---

# Doubly Linked List 이중 연결 리스트

## What is Doubly Linked List ?

In Singly Linked List, connections between nodes are one-way. However, Doubly Linked List has two-way connections between nodes. Each node has a connection to the previous node as well as a connection to the next node. That is why the Doubly Linked List is accessible to both the previous and the next nodes.

#### Structure of DDL's Node

![screen](/public/images/DDL2.PNG)

#### Structure of DDL

![screen](/public/images/DDL3.PNG)

Because the first node has no previous node, the link to the previous node is NULL. Also, because the last node has no next node, the link to the next node is NULL.

---

## Advantages of DDL

- Both previous and next accesses are possible.
- You can quickly insert a new node before a given node.
- Deletion is efficient when the pointer of a node to be deleted is given.
- It is fast to explore nodes.
  - The Singly Linked List sometimes requires all nodes to be expored when searching for a particular node.

---

## Disadvantages of DDL

- All nodes require additional space for the previous pointer.
- More memory is needed for previous pointer.
- All operations require a previous pointer.
- You have to take care of the previous pointer as well as the next pointer.

---

## When creating a new node

- When adding new data in the DDL, you must create a new node.
- The link between the previous and next node should be connected to the link of the new node.
- Finally, you need to reassign the link of the existing node.

![screen](/public/images/DDL4.PNG)

---

## When removing an existing node

- Find the position of the previous node you want to remove and reassign the 'link of the prev node' to the 'next node' of the 'node you want to remove'.
- Free the memory of the node you want to delete.

![screen](/public/images/DDL5.PNG)

---

## Implementation

[Github Link](https://github.com/HyoSup0513/study/tree/master/Datastructure/Doubly%20Linked%20List)
