---
layout: post3
title: Singleton Design Pattern
comments: true
categories: [Design Pattern]
tags: [Singleton]
toc: true
---
{:.no_toc}
## Contents

- TOC
 {:toc}
---

## What is Singleton Pattern?

Singleton Pattern is a design pattern in which one class allocates memory `only once` using `static` when an application starts, and creates `one instance` within that memory.

Even if a constructor is called several times, there is `only one object` that is actually created and the constructor that is called after the initial creation returns the object that was originally created. Use the `existing instance` instead of `creating the same instance` when it is needed.

In Java, the constructor is declared `private` so that other objects cannot be created and the object is used as `getInstance()`.

## Why use Singleton Pattern?

Create one instance using `new` and use fixed memory areas, so it is possble to avoid memory waste.

In addition, instances of a class made of singleton pattern are `global instances`, making it easy for instances of other classes to `share data`.

Therefore, Singleton pattern is a pattern for objects that require only one instance to be created. Also, Object loading times are significantly reduced when reusing instance. Therefore, Singleton pattern is better used in situations where multiple common objects must be created and used such as DBCP(Database Connection Pool).

## Problems in Singleton Pattern

If a singleton instance does too much work or shares too much data, the degree of `coupling` between instances in different classes will increase, which will violate the "open-close principle. This makes it difficult to modify and test code.

In addition, two instances can be created without synchronization in a multi-threaded environment.

## Thread-Safe Singleton Class and Instance

1. Eager Initialization (Not Thread-Safe)

- Using the characteristics of the `static` keyword, the instance is registered and used in memory through static binding at the point when the class loader initializes.
- This is `not Thread-Safe`.
- The key point is the `Singleton Pattern` should be possible to work in multi-threading environments.So, it should be Thread-Safe.

```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {}

    public static Singleton getInstance() {
        return instance;
    }
}
```

2. Lazy initialization (Thread-Safe)

- Create an instance variable with `private static`.
- The private constructor prevents the external creation of the instance.
- Use `synchronized` to make thread-safe. Ensure Thread-safe by specifying a synchronization block for the method.

However, this method is not recommended because `synchronized` cause relatively large performance degradation. Because whether an instance is created or not, it's bound to go through a sync block.

```java
public class Speaker {
    private static Speaker instance;
    private int volume;

    private Speaker() {
        volume = 5;
    }

    public static synchronized Speaker getInstance() {
        if (instance == null) {
            instance = new Speaker();
            System.out.println("Create New One");
        } else {
            System.out.println("Already Created");
        }
        return instance;
    }

    public int getVolume() {
        return volume;
    }

    public void setVolume(int volume) {
        this.volume = volume;
    }
}
```

3. Lazy initialization and Double-checked locking (Thread-Safe)

- Instead of using `synchronized` for `getInstance()`, it checks the existence of the instance with the first if statement .
- Synchronization blocks are executed only if no instance has been created.
- Therefore, this is `thread-safe` and it's possible to reduce performance reduction as it is `not affected by synchronized` block since the first instance was created.
- By using "volatile", it ensures that the variable "Instance" is initialized to the Singleton instance correctly, even if you use multi-threading.

```java
public class Speaker2 {
    private volatile static Speaker2 instance;
    private int volume;

    private Speaker2() {
        volume = 5;
    }

    public static Speaker2 getInstance() {
        if (instance == null) {
            synchronized (Speaker2.class) {
                instance = new Speaker2();
                if (instance == null)
                    System.out.println("Create New One");
            }
        } else {
            System.out.println("Already Created");
        }
        return instance;
    }

    public int getVolume() {
        return volume;
    }

    public void setVolume(int volume) {
        this.volume = volume;
    }
}
```

4. Initialization on demand holder idiom

- Uses the characteristics of `dynamic binding`.
- It does not initialize the `Holder` method, it is initialized when calling the `getInstance()` method.
- Because the instance declared in `holder` is `static`, it will only be called once at the time of class loading and the method used `final` to prevent the allocation of values again.
- Performance is superior because concurrency issues are solved without volatile or synchronized keywords.
- This is the most popular way of Singleton implementation.

```java
public class Speaker3 {
    private Speaker3() {
      volume = 5;
    }

    private static class Holder {
        public static final Speaker3 INSTANCE = new Speaker3();
    }

    public static Speaker3 getInstance() {
        return Holder.INSTANCE;
    }

    public int getVolume() {
        return volume;
    }

    public void setVolume(int volume) {
        this.volume = volume;
    }
}
```
