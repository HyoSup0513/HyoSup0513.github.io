---
layout: post
title: Difference between Process and Thread
comments: true
categories: [OS]
tags: [Process, Thread]
toc: true
---
{:.no_toc}
## Contents

- TOC
 {:toc}
---

## What is Process?

> A `process` refers a program that is currently running.

Unlike a program which is static, the process is dynamic because they are actually running.

Processes are managed directly by the kernel, and within the kernel memory there is data about the processes being managed by each process. This information is in a data structure called `Process Control Block (PCB)`, which contains the information that the kernel scheduler needs to control the process. PCB controls the operation of any process.

Process Control Block includes the following

![CQ2](/public/images/pt5.PNG)

- Process priority
- Process id
- Process State
- Program Counter
- Register
- Memory information
- List of open files
- Accounting information
- Pointer

Also, Processes are allocated independent memory areas that are structured in `Code`, `Data`, `Stack`, and `Heap` when the program runs.

![CQ2](/public/images/pt1.PNG)

- Code: Save the program's actual code
- Data: Store global, static variables defined when the process runs
- Heap: Store dynamically allocated variables during process runtime such as vars assigned within a function
- Stack: Store information about subroutines such as executing other functions in a function. (Recursion)

Because the operating system manages each process independently, there should be no overlap between different processes and no overlap of use resource areas. For example, if one process changes one part of the information in another process, it may lead to a fatal error in that process. As an exception, processes in the same program share code areas. It is better to copy several codes from the same program and refer to the code space in memory as an address rather than having each process.

At this time, various interfaces can be used to change information in a process and communication between processes is called `Inter Process Communication (IPC)`.

---

### What is Multitasking and Context switching

Simply, if we play music on a PC, and then we ran another program. We want to use other programs while listening to music. Doing various tasks simultaneously on one computer is called `Multitasking`.

Using `Time Sharing`, processes work for a very short moment to make many processes seem to work at the same time, yielding CPU resources to other processes.

However, suppose you stopped the CPU resource that were occupied by one process and gave it to another. How do processes remember what they were last doing when their turn came.

Information about the process being worked on is called `Context`. Context information is stored in the PCB when the process is switched. When each processes turn come back, they resume their work using their information stored in the PCB.

This is called `context Switching`. Unfortunately, there is a problem with this. `Overhead` can occurs because it handles tasks for CPU register status conversion, stack pointer tracking, program counter tracking. Still, many operating systems are focused on optimizing the Context Switching because the demand for multitasking is certain.

![CQ2](/public/images/pt2.PNG)

---

## What is Thread?

> Thread can be thought as a flow within a "process".

If you run a script file, then we know that each line of code will run with its own meaning.

Generally, a process begins with a single thread, which is called the main thread. Unless additional threads are generated, all programs run on the main thread.

Concurrency and multi-threading can allow multiple threads to exist within a single process. And, this means that there can be multiple flows within the running process.

But, why do we need this?

Let's suppose that there is only `one thread` and a program is running in `sequential ways`.

If we should change DB files and update files, then the first thing the program need to do is read the file, change the contents of the file, and save it to disk. These are all connected sequentially. The downside of this sequential approach is that if a task takes a long time, the `whole program can be delayed`.

There is no reason for non sequentially dependent tasks within one process to wait for the termination of another. And `multiple threads` can reduce overall working hours without getting bottlenecks.

Threads within a process share the remaining space and system resources of the process, excluding stack space, which gives the thread many advantages and disadvantages involved.

![CQ2](/public/images/pt3.PNG)

#### Advantage of using Thread

1. Thread is more efficient in term of communication between threads.
   - Because they just need to change variables that they share with each other. Communication between processes, on the other hand, is managed with its risks.
2. Thread consume less resources.
   - It doesn't need to allocate new resources because a thread share resources from existing processes with other threads.
     - The thread shares all memory except the Stack area.
     - Therefore, during context switching, the thread only handles the Stack area.
   - The `system call` to create a process and allocate resources can be reduced, enabling efficient management of resources.
3. Overall response time will be reduced.
   - The overall response is shortened due to reduced overhead. It can also distinguish between bottlenecks and other tasks, reducing overall running time.

An example of using these advantages is `HTTP communication`.

#### Disadvantage of using Thread

1. There is a possibility of collisions while using data from each other.
2. Debugging is getting a little tricky.

---

## What's the difference between process and thread?

![CQ2](/public/images/pt4.PNG)

The `process` is executed with the independently allocated memory space.
The `thread` is executed concurrently, sharing many resources within a process.

First, the process is `more independent`. They are allocated distinct resources and run without affecting other processes unless they are really needed. A thread, on the other hand, is a subset of processes and is `not independent` because multiple threads share the same process resources. In the same sense, the process has a separate address space for the resources it has, but the thread shares this address space.

Communication between processes is only possible through `IPC`, and it is relatively safe because it means that it is managed by the system. On the other hand, threads can communicate simply by modifying shared variables, making communication very easy, but they must be careful to create a safe program.

Even in context switches, threads are "generally" faster and less resource-consuming than processes. Processes produce overheads such as storing context on PCBs when they are switched.
