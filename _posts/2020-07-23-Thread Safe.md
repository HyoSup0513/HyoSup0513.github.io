---
layout: post
title: Thread Safe in OS
comments: true
categories: [OS]
tags: [Thread Safe]
toc: true
---
{:.no_toc}
## Contents

- TOC
 {:toc}
---

## What is Thread Safe?

> Thread-safe code only manipulates shared data structures in a manner that ensures that all threads behave properly and fulfill their design specifications without unintended interaction..

`Thread safe` generally means that in multi-threaded programming, there is no problem with running the program no matter what function, variable, or object is simultaneously accessed from multiple threads. In other words, when one function is called and executed from one thread, the results of the function's execution are the same, even if the other thread calls the same function and executes it together at the same time.

---

## Implementation Approaches

### 1. `Re-entrancy`

When a function is called and executed by one thread, the result must be given to each correctly, even if the other thread calls the same function.

### 2. `Thread-local Storage`

Prevent simultaneous access by reducing the use of shared resources as much as possible and using storages accessible only from each thread. Variables are localized so that each thread has its own private copy.

This method is related to the synchronization method, and is also used when sharing is unavoidable.

### 3. `Mutual Exclusion`

If shared resources must be used, access to them is controlled by locks such as semaphore.

### 4. `Atomic Operations`

Access to shared data is serialized using mechanisms that ensure only one thread reads or writes to the shared data at any time.
Mutual exclusion can be implemented by using atomic computations or by using approaches defined as 'atomic' when accessing shared resources.

---

## Synchronization with Mutex and Semaphore

Use `Mutex` for Thread and `Semaphore` for Process.

### 1. Synchronization with Mutex(Mutual exclusion)

Running Time of threads with `Critical Section` is executed separately so that they do not overlap each other.

#### Critical Section

A `Critical Section` is a code segment that accesses shared variables and has to be executed as an atomic action. So, only one process must be executing its critical section in a group of cooperating processes.

`Locking` and `unlocking` are used to coordinate access to shared resources of multiple processes. In other words, the Mutex object cannot be used simultaneously by two threads.

For example, if there is only one bathroom in the house and someone else is already inside, you have to wait until the person comes out.

```
pthread_mutex_lock(&mutx);

... Critical Section

pthread_mutex_unlock(&mutx);
```

```c
int num;

int inc(int n)
{
	num += n;
	return num;
}
```

```c
int num;
pthread_mutex_t num_lock = PTHREAD_MUTEX_INITIALIZER;

int inc(int n)
{
	pthread_mutex_lock(&num_lock);
	/* critical section */
	num += n;
	pthread_mutex_unlock(&num_lockk);
}
```

---

### 2. Synchronization with Semaphore

Semaphores can be thought of as a simple counter to indicate the status of a resource. Generally, they are used for resources that have relatively long time. Semaphores support only three atomic operations: `Initialize`, `increment`, `decrement`. And, a semaphore uses two atomic operations, `wait` and `signal` for process synchronization

There are mainly two types of semaphores such as `counting semaphores` and `binary semaphores`.
Semaphores use binary digits (0 or 1) or have additional values according to type. The process of using semaphores should usually check the values and change them while resources are being used so that other semaphores can wait.

Semaphore can be compared to the number of keys to an empty room in a hotel. In other words, assuming that there is as much key as an empty space, the number of keys decreases every time people enter the room. When the room is full, the count will be zero and the next guest will wait until one of the room is empty.

---

`S` is an integer value variable and can be accessed jointly by a procedure called `P` and `V`.

P has a structure in which something is performed before entering a critical section, and V has a structure in which something is performed when leaving the critical section. `P` decreases `S`, `V` increases `S`.

However, if the condition `S<=0` in `P` is satisfied, `P` becomes waiting state unless V is called. This is Semaphore's concept.

```
P(S) {
     while (S <=0); // Do nothing
     S--;
 }

 V(S) {
     S++;
 }
```

This can be improved as shown in the code below.

```
P(S) {
     S--;
     if (S < 0)
         // wait status
 }

 V(S) {
     S++;
     if (S <= 0)
         // wakeup status
 }
```

For S with an initial value of 1, P operates as a wait object and V operates as a signal. This creates a structure in which different procedures can signal using Semaphore.

---

## Mutex vs Semaphore

1. A `binary semaphore` can be used as a `Mutex` but a `Mutex` can never be used as a `semaphores`. Mutex is a binary semaphore with only two states of `0 and 1`.
2. Mutex is an `object` while Semaphore is an `integer`.
3. Semaphores are `not allowed to own`, while Mutex is `allowed to own` them and the owner is responsible for them.
4. Semaphores exist in the form of files in the file system. Mutex, on the other hand, has a range of processes and is automatically cleaned up at the end of the process.
5. The biggest difference is the number of synchronization targets managed. Mutex is used when there is `only one` synchronization target and semaphore when there is `more than one` synchronization target.
