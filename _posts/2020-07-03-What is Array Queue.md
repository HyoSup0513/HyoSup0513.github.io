---
layout: post
title: What is Array Queue?
comments: true
categories: [Data Structure]
tags: [Array Queue, C]
toc: true
---

{:.no_toc}

## Contents

- TOC
  {:toc}

---

## What is Queue and How it works?

- Queue is a sequential structure that store data linearly.
- The order is `FIFO`(First In, First Out).
- When adding new data, add it to the `rear` location.
- When removing existing data, remove the data from the `front` location.
- Queue can be thought of as a `horizontal` structure.

![CQ2](/public/images/AL2.PNG)

## Structure of Array List

- Array Queue is implemented using `array`.
- Array Queue has `front` and `rear`.
  - The insertion of data occurs at `front`.
  - The deletion of data occurs at `rear`.

![CQ2](/public/images/AL2.PNG)

---

### Advantage of Array List

- It takes O(1) to get the element in the array.

### Disadvantage of Array List

- The size of the array is `fixed`, so you cannot insert more elements than the size of the array.
  - `Resize` is required when larger size array is needed.
- The empty space cannot be filled when the `front pointer` moves ahead.

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

### Peek

- We can easily find it by using the `location of the data` we want to find.

![CQ2](/public/images/AL5.PNG)

### Implementation

[GitHub](https://github.com/HyoSup0513/study/blob/master/Datastructure/List/Array%20list.c)
