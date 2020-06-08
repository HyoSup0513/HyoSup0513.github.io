---
layout: post
title: Array Stack (배열 스택)
comments: true
categories: [Data Structure]
---

# Array Stack 배열 스택

## What is Stack ?

- Sequential Structure like list data structure.
- Unlike the list data stucture, it is a LIFO.
  - Addition and removal of data is made in TOP.

---

## Operations for Stack

- Pop - Remove the data in the Top of the stack and return it.
- Push - Add data to the Top of the stack.
- Peek - Returns the data at the Top of the stack. (Not actually removing)
- isEmpty - Check if the stack is empty.

---

## Advantages of Stack

- Speed is very fast.
  - It is possible to access nodes faster.

---

## Disadvantages of Stack

- The number of data to be stored should be estimated and the stack should be sized at leisure.
  - It is to add data later. If the array is sized by the number of data, it will not be able to add new data later.
- Therefore, memory can be wasted.

---

## How does the Array Stack work?

- The data in the array stack is stored on the node.

  - You can store data on a node and store multiple data.

    ![stackimg1](/public/images/astack2.PNG)

- The first data inserted becomes the oldest data.
- When new data is inserted, the data becomes top.
- When speicific data is removed, the data in the top is removed and the new top is determined.

#### How the stack works

![stackimg2](/public/images/astack1.PNG)
---
## When inserting new data

- As new data is inserted, the top's position index increases by 1.
- Make sure the array is full or not.

  ![stackimg3](/public/images/astack3.PNG)
---
## When removing existing data

- When data is removed, the data in the top is removed and the node below the existing data becomes the top.
- Therefore, the location index of the top should be reduced by 1.
- Make sure if there is any data that can be removed.

  ![stackimg4](/public/images/astack4.PNG)
---
## Implementation

[Github](https://github.com/HyoSup0513/study/blob/master/Datastructure/Stack/Array%20Stack.c)
