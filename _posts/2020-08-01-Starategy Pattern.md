---
layout: post3
title: Strategy Pattern
comments: true
categories: [Design Pattern]
tags: [Strategy]
toc: true
---
{:.no_toc}
## Contents

- TOC
 {:toc}
---

## What is Strategy Pattern?

> Strategy lets the algorithm vary independently from clients that use it.

![CQ2](/public/images/STP1.PNG)

- `Context` : A role that uses Strategy. Context has and uses Concrete Strategy's Instance.
- `Strategy`: Defines an interface for using the strategy.
- `Concrete Strategy`: Each subclass implements a Strategy's interface.

By creating a strategy class for each behavior that objects can do, and defining an interface that encapsulates similar behaviors.

Each of the behaviors that an object can perform is made into a strategy, and if it needs to be modified dynamically, it can be modified by simply changing the strategy.

---

## Why use Strategy Pattern?

1. When there are many classes that are conceptually related, with only slightly different behaviors.
2. When a transformation of an algorithm is required.
3. When a class defines many behaviors, it is better to move the conditional statement to the Strategy class than to use many conditional statements in one class.

When we play a game called League of Legends, each champion can be equipped with various runes.

For example, suppose we have classes called `Ryze` and `Darius`, and these two classes implement the Champion interface.
(Ryze and Darius are game characters.) And the `Client` uses two objects.

```java
public interface Champion {
    public void setRune();
}

public class Ryze implements Champion{
    public void setRune(){
        System.out.println("Equip Electrocute rune.")
    }
}

public class Darius implements Champion{
    public void setRune(){
        System.out.println("Equip Conqueror rune.")
    }
}

public class Client {
    public static void main(String args[]) {
        Champion ryze = new Ryze();
        Champion darius = new Darius();

        ryze.setRune();
        darius.setRune();
    }
}
```

In the above example, Ryze uses `Electrocute` rune and Darius uses `Conqueror` rune.
However, the `setRune` method of each champion must be modified to change the rune used by each champion.

```java
    public void setRune(){
        System.out.println("~~~")
    }
```

But this is a violation of the principle of SOLID design, Open-Closed Principle (OCP). The behavior should be changed without modifying the `setRune` method directly.

Also, when using various champions, all champions use their own `setRune` method. Therefore, the same method is defined equally in many classes, resulting in duplication of methods.

Therefore, we use a `Strategy Pattern` to solve these problems.

Because the implementation of the context class and the implementation of the algorithm are separated independently from each other, it is easy to maintain and expand the code, and can change the algorithm dynamically.

---

## Problems

- Client should know the differences between each other about the subclass of strategy.
- Context, strategy, and their subclasses are associated for data reference, resulting in higher degree of coupling.
- There is a communication overhead between the Strategy object and the Context object.

---

## Example

### Simple structure of the game

- Champions
  - Ryze
  - Darius
  - ...
- Runes
  - Precision
    - Conqueror
    - Press the Attack
    - ...
  - Domination
    - Electrocute
    - Predator
    - ...
  - Sorcery
    - Arcane Comet
    - Phase Rush
    - ...
  - ...

---

First, create a strategy.

Among the five rune types, there are Precision, Domination, and Sorcery, and others.
So, create a strategy according to the types of rune. (Precision, Domination, Sorcery)

And the three classes implement the `setRune` method to determine which rune is used.
Also, cretae an `RuneStrategy` interface to encapsulate these three strategy classes.

This makes it easier to add other strategies later.

```java
public interface RuneStrategy {
    public void setRune();
}

public class PrecisionStrategy implements RuneStrategy {
    public void setRune() {
        System.out.println("Equip Conqueror rune.");
    }
}

public class DominationStrategy implements RuneStrategy {
    public void setRune() {
        System.out.println("Equip Electrocute rune.");
    }
}

public class SorceryStrategy implements RuneStrategy {
    public void setRune() {
        System.out.println("Equip Arcane Comet rune.");
    }
}
```

---

Next, let's define the class for the champion.

All champions can set the run through the `setRune` method.

Instead of directly implementing the method of setting the rune, set up a strategy for which rune to be used, then use the algorithm of the strategy to equip the rune.

So there exists `setRuneStrategy`, a method for setting strategies.

```java
public class Champion {
    private RuneStrategy runeStrategy;

    public void setRune() {
        runeStrategy.setRune();
    }

    public void setRuneStrategy(RuneStrategy runeStrategy) {
        this.runeStrategy = runeStrategy;
    }
}

public class Ryze extends Champion {

}

public class Darius extends Champion {

}
```

---

Finally, implement the `Client` class using the `Ryze` and `Darius` objects.

After creating the `Ryze` and `Darius` objects, call the `setRuneStrategy` method to set which rune each champion will use.

Use domination rune type for `Ryze` and precision rune type for `Darius`. Also, the rune of `Ryze` can be flexibly modified.

```java
public class Client {
    public static void main(String args[]) {
        Champion ryze = new Ryze();
        Champion darius = new Darius();

        System.out.println("[Ryze]");
        ryze.setRuneStrategy(new DominationStrategy());
        ryze.setRune();

        System.out.println();
        System.out.println("[Darius]");
        darius.setRuneStrategy(new PrecisionStrategy());
        darius.setRune();

        System.out.println();
        System.out.println("[Ryze]");
        ryze.setRuneStrategy(new SorceryStrategy());
        ryze.setRune();
    }
}
```

#### Output

![CQ2](/public/images/STP2.PNG)

---

## Implementation

[Github](https://github.com/HyoSup0513/study/tree/master/Design%20Pattern/Strategy%20Pattern)
