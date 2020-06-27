---
layout: post
title: What is Hash and Hash Table
comments: true
categories: [Data Structure]
tags: [Hash Table, C++]
toc: true
---
{:.no_toc}
## Contents
* TOC
{:toc}
---

# About Data Structure Hash Table

## What is Hash Table ?

The Hash Table consists of `key`, `value`, `hash function`, `hash`, `Bucket`.

- `Hash Table` is a data structure that uses an `associative array structure`.
  - Associative array
    - An array in which one key and one data are paired 1:1.
    - Value can be derived using the key.
- `Keys` and `Values` are paired.
- Use `Hash function` to compute index(aka `Hash Code`) using Key values into an array of `buckets`.

---

## Structure of Hash Table

![CQ2](/public/images/hashtable1.PNG)

- Key : Key a unique value and input of hash function.
- Value : The value that is finally stored in a bucket and it must be paired with a key.
- Hash function : Compute the key to hash code.
- Hash or Hash code : The result of a hash function and stored in a bucket paired with a value.
- Bucket or Slot - Where the values are stored.

#### The `key` is computed to `hash` via `hash function` and the hash is matched with `value` and stored in the `bucket`.

## Basic Operations for Hash Table

- Search - Search a value with a key.
- Insert - Compute key to hash through hash function and insert data.
- Delete - Delete a hash and value that matches a key.

But, there is a problem with `Hash function`.

#### Probelm with Hash Function

1. Hash Collision : When different keys become the same hash code through a hash function, it is called `Hash Collision`.
2. Overflow : If hash collisions occur more than the number of slots allocated to buckets, no more values can be inserted in buckets.
3. Clustering : When data is concentrated in one record, it is called clustering.

In some cases, the value of all buckets may have to be looked up due to `Hash Collision`.

![CQ2](/public/images/hashtable2.PNG)

So, Time Complexity of Search, Insertion, and Delete => Best Case : `O(1)`, Worst Case : `O(N)`

Therefore, it is important to create a function that reduces the probability of a hash collision as much as possible.

---

## Collision Resolution

## Separate Chaining

![CQ2](/public/images/hashtable3.PNG)

- In the separate chaining, each bucket is independent.
- Each bucket has some sort of list of entries with the `same index`.
- Use `linked list` data structure.
- When a collision occurs in a bucket, it `links new data` next to the `existing data`.

### Change of Operations

#### Search

- Find the index through a hash function.
- Linearly check the list of connections in the corresponding index to see if the node of the key exists and return the value.

#### Insertion

- Insert a node to the linked list indicated by an index mapped with a key, and add a value to that node.

#### Deletion

- Linearly check the linked list of the corresponding index, delete the node of the corresponding key.

---

### Advantage of Separate Chaining

- Limited bucket can be used efficiently.
- Use less memory because there is no need to allocate space in advance.
- The use of linekd list reduces the constraints of data that can be added.

### Disadvantage of Separate Chaining

- Search efficiency is reduced when various keys have the same hash and one bucket has multiple entries.
- Requires additional memory to use linked list.
- Worst case of Separate chaining is `all nodes are inserted into the same bucket`.

#### It is better to use Chaining when it is unknown `how many and frequently` keys many be inserted or deleted.

---

## Open addressing

- Open addressing is a method that finds empty bucket and stores data.
- Hash table are maintained in a form where one hash and one value are matched.
- When a collision occurs in a bucket, the `index(hash)` is changed to store it in another bucket.

### Change of Operations

#### Deletion

- If we just delete a key, then search may not be worked.
- To prevent this, insert a `Dummy node(deleted)` in the deleted location. So, it is possible to `connect to the next index` when searching.
- If the number of dummy nodes increases, `rehashing` is required to avoid performance reduction.

---

### Advantage of Open Addressing

- Because no additional storage is needed, no additional work is required.
- By not using a pointer, `serialization` is easy.

### Disadvantage of Open Addressing

- The performance of a hash table depends on the performance of a hash function.
- The number of stored nodes cannot exceed the number of slots in the bucket array.

## Probe Sequence of Open Addressing

### 1. Linear Probing

![CQ2](/public/images/hashtable4.PNG)

- Linear Probing stores keys in the first empty bucket by `searching the empty space linearly` according to specific interval (usually 1) from the original index to.
  - hash + 1
- When you reach the end of the table, go back to the beginning of the table.
- Good CPU cache utilization
- However, in the worst case, it is inefficient and most vulnerable to `clustering of data` because it may require searching the entire hash table.

### 2. Quadratic Probing

![CQ2](/public/images/hashtable5.PNG)

- Primary clustering of linear probing can be solved, but `secondary clustering` can occur.
- Probe is calculated by adding `ouptut of a quadratic poly nomial` to the original index.
- Quadratic probing stores keys in the first empty bucket by searching empty space as far as `i^2` from original index.
  - hash + 1, hash + 2, hash + 9

#### What is Primary Clusting and Secondary Clusting

![CQ2](/public/images/hashtable8.PNG)

- Primary Clusting: After a hash collision, two of the keys in the hash table is hashed to the same position, and one of the keys is moved to the next position. Once this happens, the newly added keys also have the chance of experiencing another hash collision, even though the hash values are different.

  - Primary Clusting causes `searching time of key` within the cluster to be longer.
  - Especially `linear probing`

- Secondary Clusting: Secondary clusting is occured when a low-quality hash function computes keys to same hash, then they will follow the same probe sequence or be placed in the same hash chain.
  - Especially `linear probing` and `quadratic probing`

### 3. Double Probing

![CQ2](/public/images/hashtable6.PNG)

- Probe is calculated by a `second fash function` when a hash collision occurs.
- The efficiency of CPU cach utilization is reduced but has little impact on clustering.
- However, more computation is required.

#### It is better to use Open Addressing when it is known `how many and frequently` keys many be inserted or deleted.

---

## Resizing

![CQ2](/public/images/hashtable7.PNG)

- If the number of entries in a hash table exceeds the current capacity, then the hash table have to be rehashed.
- Rehashing means increasing the size of data structure and mapping existing datas to new bucket locations.
- Resizing
  - In Separate Chaining, increase the number of buckets.
  - In Open Addressing, increase the size of fixed-size arrays.

#

#### Implementation

Chaining Hash Table [GitHub](https://github.com/HyoSup0513/study/blob/master/Datastructure/Search/ChainingHashTable.cpp)
