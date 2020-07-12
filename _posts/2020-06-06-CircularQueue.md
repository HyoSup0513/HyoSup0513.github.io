---
layout: post
title: What is Circular Queue
comments: true
categories: [Data Structure]
tags: [Queue]
toc: true
---

## Why use Circular Queue?

- Improve memory overflow of array queue
  - Even if there's a an empty node at the front, memory overflow occurs when we try to enqueue a new node.
  - We can use the method of moving the array. However, beacuse the time complexity is O(N), it is a problem in a large array to move the array.
  - Circular Queue is an efficient way to do this.

## ![CQ1](/public/images/CQ2.PNG)

It is impossible to add a new node even if there is an empty node in Front.
To insert a new node into the Front, the existing nodes A, B, and C must be moved from 1, 2, 3 to 0, 1, 2.
But this process is not necessary in Circular Queue, because circular queue connect Front and Rear.

---

## Characteristic of Circular Queue

- Connect the front and rear of the array.
  - To connect the front and rear, use 'mod' operator to move the rear node.
  - rear = (rear + 1) % array size

![CQ2](/public/images/CQ1.PNG)
A is removed from index 0 by Dequeue(A), and then Front is changed to B in index 1.
Then, Enqueue(E) inserts E into index 0 with empty node, and E becomes the new Rear.

---

# Implementation

[Github](https://github.com/HyoSup0513/study/blob/master/Datastructure/Queue/CircularQueue.c)
