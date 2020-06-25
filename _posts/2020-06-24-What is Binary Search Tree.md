---
layout: post
title: What is Binary Search Tree
comments: true
categories: [Data Structure]
<<<<<<< HEAD
tags: [Hash Table, C++]
toc: true
=======
tags: [Binary Search Tree, C]
>>>>>>> 8f82c63c9e2b17e1c0e2deb978051f232f1fab6f
---

# About Data Structure Binary Search Tree

## What is Binary Search Tree ?

- Use [Binary Tree](https://hyosup0513.github.io/data%20structure/2020/06/11/Types-of-Binary-tree.html) data structure
- Every node can have a `maximum of two children`.
- The `left subtree of a node` consists of nodes with values `less than the node's value`.
- The `right subtree of a node` consists of nodes with values `greater than the node's value`.
- Both the left subtree and the right subtree are binary search trees.

![CQ2](/public/images/bst1.PNG)

---

## Abstract data types of BST

- Create BST - Create new binary search tree.
- Insert data - Add a new node.
- Delete data - Remove a existing node.
- Search - Returns the node corresponding to a specific key.
- Delete BST - Delete the binary search tree.

### Basic Operations

### Search

![CQ2](/public/images/bst2.PNG)

1. If the key value you are looking for `matches` the key value of the current node : Search succeeded, `return the current node`.
2. If the key value you are looking for is `less` than the key value of the current node : Move to `left subtree`.
3. If the key value you are looking for is `larger` than the key value of the current node : Move to `right subtree`.

---

### Insertion

![CQ2](/public/images/bst3.PNG)

1. Search for a location to add data to : Locate the parent node.
2. Add a new node to the found location.

---

### Deletion

#### Three Delete Cases

1. There are `no child nodes` of the node you want to remove.

![CQ2](/public/images/bst4.PNG)

If the node you want to remove does not have a child node, you can see that the node you want to remove is a `leaf node`. Therefore, removing a node is simple.

`Remove the node you want to remove` and set the connection to the parent node pointing to the removed node to `null`.

2. There is `one child node` of the node that you want to remove.

![CQ2](/public/images/bst5.PNG)

If the node you are trying to remove has one child node, additional processing is required on the child node.

Move the `child node of the node to be removed` to the `location of the node to be removed`.

The `parent node` of the node to be removed is connected with the `child node` of the node to be removed.

3. There is `two child nodes` of the node that you want to remove.

![CQ2](/public/images/bst6.PNG)

If you remove node 100 with two child nodes, you must replace node 100 with a specific node.

A spcfic node can be

1. the largest node in the left subtree of the node to be removed.
2. the smallest node in the right subtree of the node to be removed.

![CQ2](/public/images/bst7.PNG)

Therefore, you can choose between 70 or 120.
If we choose 70, remove node 100 and insert 70 at node 100 position.

![CQ2](/public/images/bst8.PNG)

Then replace the position on node 70 with child node 60 on node 70.
