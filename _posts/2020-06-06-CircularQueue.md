---
layout: post
title: Circular Queue 원형 큐
comments: true
categories: [Database]
---

# Array Circular Queue 배열 원형 큐

## Why use Circular Queue?

- Improve memory overflow of array queue
  - Even if there's a an empty node at the front, memory overflow occurs when we try to enqueue a new node.
  - We can use the method of moving the array. However, beacuse the time complexity is O(N), it is a problem in a large array to move the array.
  - Circular Queue is an efficient way to do this.

## ![CQ1](/public/images/CQ2.PNG)

## Characteristic of Circular Queue

- Connect the front and rear of the array.
  - To connect the front and rear, use 'mod' operator to move the rear node.
  - rear = (rear + 1) % array size

![CQ2](/public/images/CQ1.PNG)

# Implementation

[Github](https://github.com/HyoSup0513/study/blob/master/Datastructure/Queue/CircularQueue.c)
