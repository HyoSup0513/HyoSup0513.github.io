---
layout: post
title: What is Array Stack?
comments: true
categories: [Data Structure]
tags: [Array Stack, C]
toc: true
---
{:.no_toc}
## Contents

- TOC
 {:toc}
---

## What is Stack and How it works?

- Stack is a sequential structure that store data linearly.
- The order is `LIFO`(Last-In, First-Out).
- Adding and removing data is done in the `top` of the stack.
- Stack can be thought of as a `vertical` structure.

![CQ2](/public/images/stack11.PNG)

![CQ2](/public/images/stack2.PNG)

## Structure of Array Stack

- Array Stack is implemented using `array`.
- Array Stack has `top`.
  - The insertion and deletion of data occurs in the top.

![CQ2](/public/images/stack3.PNG)

---

### Advantage of Array List

- It takes O(1) to get the element in the array.

### Disadvantage of Array List

- The size of the array is `fixed`, so you cannot insert more elements than the size of the array.
  - `Resize` is required when larger size array is needed.
- The empty space cannot be filled when the `front` moves ahead.

---

## Operations for Array Stack

- Calculate the `top` using the variable `curretCount`.

### Push

- The new data is inserted into the `location of top + 1`.
  - The location index of the `top` can be found by the variable `currentCount`.
  - CurrentCount is a variable that means the current number of nodes.
  - `Top = currentCount - 1`
- Therefore, the location index where the new data will be inserted is the `currentCount`.
- If `currentCount` is equal to `maxCount`, the stack is full.
- After inserting the data, increase the number of nodes by 1.
  - currentCount++;

```c
// Insert new data into the top.
pStack->pData[pStack->currentCount].data = data;
// Increase the variable currentCount indicating the current number of nodes.
pStack->currentCount++;
```

![CQ2](/public/images/stack4.PNG)

### Pop

- Remove the node on the Top.
  - The location of the top is currentCount - 1.
- After removing the node in the `top`, reduce the number of nodes by 1.
  - currentCount--;

```c
// Set the node to return.
pReturn->pData = pStack->pData[pStack->currentCount - 1]
// Decrease the variable currentCount indicating the current number of nodes.
pStack->currentCount--;
```

![CQ2](/public/images/stack5.PNG)

### Peek

- Peek only returns the node in the top without removing it.
- Returns the node located in the Top.
  - Top = curretCount-1.

```c
pReturn = &(pStack->pData[queue->currentCount - 1]);
```

![CQ2](/public/images/stack6.PNG)

### Implementation

[GitHub](https://github.com/HyoSup0513/study/blob/master/Datastructure/Stack/Array%20Stack.c)
