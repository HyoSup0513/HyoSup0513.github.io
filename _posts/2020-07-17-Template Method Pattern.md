---
layout: post3
title: Template Method Pattern
comments: true
categories: [Design Pattern]
tags: [Template Method]
toc: true
---
{:.no_toc}
## Contents

- TOC
 {:toc}
---

## What is Template Method Pattern

> Template Method Pattern defines the skeleton of an algorithm in a method, deferring some steps to subclasses. Template Method lets subclasses redefine certain steps of an algorithm without changing the algorithms structure. – GoF Design Patterns

![CQ2](/public/images/TM2.PNG)

- `AbstractClass` : A class that defines a template method. AbstractClass defines a common algorithm of subclasses and the functions that will be implemented in a subclass as primitive methods or hook methods.
- `ConcreteClass` : A class that implement inherited primitive or hook methods. ConcreteClass overrides the primitive or hook methods to suit the subclass.

---

## Why use Template Method Pattern?

It is useful when `minimizing code duplication` of a method that is the same overall but partly different.

- Template Method Pattern defines the same functionality in the superclass, allowing only the parts that need to be expanded or changed to be implemented in the subclass.
- Template Method Pattern implements common algorithms in the superclass, and implements different algorithms in subclasses. Therefore, it is useful for reusing the overall algorithm code.

---

### Problems

1. If there are too many abstract method that Concrete Class must implement, management becomes `complicated`.
2. When there are many subclasses managed by a superclass , if the superclass is modified, `all subclasses` must be modified `individually`.

---

## Example

When we play any rpg game, there are many `Classes` such as DPS, Tank, Healer, etc.
The role of `DPS` is to increase damage and kill monsters quickly. They also usually use long-range weapons because they have to be at a safe distance from monsters. The role of a `tank` is getting an attack from a monster to protect party members. Therefore, defense will be important. Finally, the role of the `healer` will be to restore the injury of the party members.

- Classes (AbstractClass)
  - Tank (ConcreteClass)
  - DPS (ConcreteClass)
  - Healer (ConcreteClass)

---

```java
public abstract class Classes {

    void readyToBattle() {
        repairWeapons();
        prepareWeapon();
        prepareArmor();
        if (isUsingPrepareOther()) {
            prepareOther();
        }
    }

	final void repairWeapons(){
		System.out.println("Repair weapons..");
    }

    abstract void prepareWeapon();

    abstract void prepareArmor();

    // If you want to prepare something else, you have to change it to 'true'.
    boolean isUsingPrepareOther() {
        return false;
    }

    // Override 'isUsingPrepareOther' value to use.
    void prepareOther() {
    };
}
```

Creates an abstract class called `Classes` that defines all classes.

All Classes need to repair their weapons before a fight, `abstract` keyword is not used in `repairWeapons` method.

Create a `hook method` for a class that requires different preparation. `isUsingPrepareOther` can be used for classes that require different preparation.

When the `readyToBattle` method is executed, the remaining methods are executed in turn.

---

```java
public class Tank extends Classes {
    @Override
    void prepareWeapon() {
        System.out.println("Equip a sword and shield.");
    }

    @Override
    void prepareArmor() {
        System.out.println("Wear metal armor.");
    }

}
```

The `tank` class uses swords and shields, and wears metal armor. So, let's just prepare the weapons and the armors.

---

```java
public class DPS extends Classes {
@Override
void prepareWeapon() {
System.out.println("Equip a bow and a quiver.");
}

    @Override
    void prepareArmor() {
        System.out.println("Wear leather armor.");
    }

    @Override
    boolean isUsingPrepareOther() {
        return true;
    }

    @Override
    void prepareOther() {
        System.out.println("Put arrows into the quiver.");
    }

}
```

Let's suppose there is a archer in dps class.
The `DPS` class uses a bow and quiver or a gun, and wears leather armor to move quickly. Also, use `hook method` to prepare arrows.

---

```java
public class Healer extends Role {
    @Override
    void prepareWeapon() {
        System.out.println("Equip a Wand");
    }

    @Override
    void prepareArmor() {
        System.out.println("Wear a robe.");
    }

    @Override
    boolean isUsingPrepareOther() {
        return true;
    }

    @Override
    void prepareOther() {
        System.out.println("Put the potions in the bag.");
    }
}
```

`Healer` uses a a wand, and wears a robe. Healers also need to pack enough potions.

---

Lastly, let's test the pattern.

```java
public class TemplateMain {
    public static void main(String[] args) {

        System.out.println("[Tank]");
        Tank class01 = new Tank();
        class01.readyToBattle();
        System.out.println();

        System.out.println("[DPS]");
        DPS class02 = new DPS();
        class02.readyToBattle();
        System.out.println();

        System.out.println("[Healer]");
        Healer class03 = new Healer();
        class03.readyToBattle();
    }
}
```

![CQ2](/public/images/TM3.PNG)

---

## UML diagram

![CQ2](/public/images/TM1.PNG)

## Implementation

[Github](https://github.com/HyoSup0513/study/tree/master/Design%20Pattern/Template%20Method%20Pattern)
