---
layout: post
title: What is Array List?
comments: true
categories: [Data Structure]
tags: [Array List, C]
toc: true
---
{:.no_toc}
## Contents

- TOC
 {:toc}
---

## What is Array List?

- Array List is a data structure that implements the list using an array.
- Sequential Structure

  - stores data in order.

  ![CQ2](/public/images/AL1.PNG)

## Structure of Array List

- Data is stored within the node.
  - Multiple data can be stored.
- Every element has its own address.
  - So, the address of a particular element can be calculated.

![CQ2](/public/images/AL2.PNG)

---

### Advantage of Array List

- It takes O(1) to find a data in a particular location.
  - It is fast to access certain data using indexes.
- `Random access` is possible, it's easy to access nth element.
- Memory is allocated in `contiguous memory location` for its data.
  - It's possible to avoid `memory overflow` or shortage of memory.
- It is simple to implement.

### Disadvantage of Array List

- The size of the array is `fixed`.
  - When the array is full, it's not possible to add new data.
  - Therefore, an `array of larger sizes` than `the number of data to be stored` must be created, which is a `waste of memory space`.
  - If the array is smaller than the number of data to be stored, it can cause problems.
- The time complexity of adding and deleting data is O(N).

---

## Operations for Array List

### Insertion

- If we simply add new data, add the data from the `left side of the array` sequentially.
- However, if new data is added where the `data already exists`, all existing data `must be moved`.
  - Move the data on the right first.

![CQ2](/public/images/AL3.PNG)

### Deletion

- The data on the right can be easily removed.
- However, if we remove the data in the middle, we have to `fill in the empty space`.

![CQ2](/public/images/AL4.PNG)

### Get Data

- We can easily find it by using the `location of the data` we want to find.

![CQ2](/public/images/AL5.PNG)

### Implementation

[GitHub](https://github.com/HyoSup0513/study/blob/master/Datastructure/List/Array%20list.c)
