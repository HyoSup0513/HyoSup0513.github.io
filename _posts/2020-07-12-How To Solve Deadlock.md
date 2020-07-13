---
layout: post2
title: How To Handle Deadlock?
comments: true
categories: [OS]
tags: [Deadlock]
toc: true
---
{:.no_toc}
## Contents

- TOC
 {:toc}
---

## What is Deadlock?

![CQ2](/public/images/deadlock1.PNG)

> Deadlock can occur when you try to use limited resources in many places.

In the multi-programming environment of a computer system, multiple processes compete to use limited resources, and when a process requests resources, a deadlock occurs when those resources are not available. This means that the requested resources are occupied by other processes, and the processes they occupy are queued for other resources, so the two processes cannot escape the waiting state is called deadlock.

---

### System Model

The system consists of a finite number of resources to be distributed among competing processes for resources such as CPU, Memory, and files, I/O devices.
In order for a process to use resources, a `request must be made` before the resource is used and `release the resouce` after the resource is used.

Normally, the process can only use resources in the following order

1. `Request` : The process requests resources and, if they are not immediately available, waits until they are available.
2. `Use` : Task is carried out using resources.
3. `Release` : When the processes complete their tasks, then releases the resources.

---

### Four Conditions for Deadlock

A deadlock occurs when the following four conditions are established simultaneously within a system. However, if one of the four conditions is insufficient, no deadlocks will occur.

1. `Mutual exclusion` : To allow a process to use resources mutually exclusive so that they cannot be used simultaneously with other processes. Only one process can use the resource at any given instant of time.
2. `Hold and wait` : A process is currently holding at least one resource and requesting additional resources which are being held by other processes.
3. `No preemption` : Resources cannot be forcibly released, and the occupied process can only be released voluntarily by the process after it terminates the task.
4. `Circular wait` : Each process must be waiting for a resource which is being held by another process cyclically.

---

## How to Handle Deadlock ?

1. First, using a protocol to `prevent` or `avoid` deadlock.
2. Second, `detecting` a deadlock in the system, and then `restore` it.
3. Thrid, making it look like `it doesn't happen`, ignoring the system's deadlock.

Most systems do not experience a lot of deadlock. Also, it costs a lot for preventing, avoiding, detecting and recovering the deadlock. In some cases, it seems like a deadlock situation even though no deadlock has occurred.

### Deadlock Prevention

`Deadlock Prevention` is a method of resolving the deadlock by removing one of the conditions.

#### 1. `Mutual exclusion`

The first requirement of the deadlock, mutual exclusion, is due to resources that cannot be shared. If multiple processes open a read-only file, the processes are guaranteed simultaneous access to the file, which can break the mutual exclusion and prevent a deadlock. However, some resources may not be shared fundamentally, so mutual exclusion must occur, which may not prevent a deadlock.

#### 2. `Hold and wait`

To avoid "Hold and wait", ensure that processes do not occupy other resources when requesting resources. That is, if you allow a process to request other resources only when it has no resources, the process itself does not occupy any resources, so "Hold and wait" will not occur even if it waits.

The protocol that is available in this case is to request and assign all necessary resources before the process runs. This eliminates waiting for processes to request and receive other resources to be allocated to the extent, and no waiting occurs because they start the process with all the resources.

Another protocol is to allow a process to request resources only when it does not occupy resources. In this case, no "Hold and wait" occurs because the process never occupies resources when it waits for resources.

#### 3. `No preemption`

No preemption means that resources cannot be forcibly released. One way to do prevent this is to break the deadlock by forcing the resources occupied by the process to be released, allowing other processes to use resources.

If a process occupying a resource requests another resource that cannot be immediately preepmted, all resources currently occupied by that process are released and preepmted to other processes in need. The process will only resume if it can reacquire the new resources it is requesting, as well as the old resources it is currently forced to release.

#### 4. `Circular wait`

To eliminate circular wait, set order for all resources and have each process request resources in the prescribed order. This prevents a deadlock because all resources are preepmted in a fixed order.

---

### Deadlock Avoidance

Deadlock Avoidance is a way of allocating resources only when there is no possibility of a deadlock occurring.

One of the most representative algorithms is the `Banker's algorithm`.

#### `- Banker’s Algorithm`

Banker's algorithm is a technique that avoids deadlock by checking in advance whether a system remains stable after allocating resources when a process requires resources.
The method is proposed by `Edsger Dijkstra` and a technique derived from the allocation of cash by banks to meet all customers' needs. `Safe state` and `unsafe state` are needed to determine whether there is a possibility of a deadlock. When in `safe state`, allocate resources, otherwise wait for other processes to release resources.

##### `- Safe State`

`Safe State` means that no matter in which order the process requests resources, they can all be allocated well without causing a deadlock. The avoidance algorithm ensures that the system is always in a safe state within the specified maximum resources. To do this, when processes request resources, they decide whether to accept the request or to wait to avoid a deadlock, only if the system can remain stable.

---

### Deadlock Detection

An operating system detects a deadlock using a detection algorithm. Also, the `resource allocation graph` is used to detect a deadlock.

1. Resources have single instance

   - ![CQ2](/public/images/deadlock2.PNG)

   - In this Graph, there is a cycle R1->P1->R2->P2. And, it is the sufficient confition for deadlock.

2. Resources have multiple instances

   - ![CQ2](/public/images/deadlock3.PNG)

   - In this case, we have to construct allocation matrix and request matrix to judge deadlock.

---

### Deadlock Recovery

Recovery means releasing the resources preempted, or terminating the process that caused the deadlock.

#### `- Process Termination`

1. Abort all the Deadlocked Processes.
   - This method costs a lot. Because the process must have worked a lot until the deadlock, and if this results are discarded, you have to start calculating again.
2. Abort one process at a time untill deadlock is eliminated.
   - This method creates significant overhead because when each process is aborted, you need to check whether any processesares still deadlocked.

#### `- Resource Preemption`

To eliminate a deadlock through `Resource Preemption`, we have to continue to preempt resources from the process and give them to other processes until the deadlock is resolved.

The following matters should be considered:

1. `Selecting a victim`
   - You have to think about which resources and which processes will be preempted. In order to minimize costs, victims should be chosen in consideration of variables such as the number of resources preempted by the deadlock process and the amount of time it has taken to run so far.
2. `Rollback`
   - If a process is forced to release resoruces and the resources are preempted, it is necessary to consider how to handle the process. Usually the safest way is to stop and restart the process(Roll back).
3. `Starvation`
   - In some case, the same process is likely to continue to be selected as a victim. In this case, the process may fall into a starvation where a task is never completed. One solution is that a process must be picked as a victim only a finite number of times.
