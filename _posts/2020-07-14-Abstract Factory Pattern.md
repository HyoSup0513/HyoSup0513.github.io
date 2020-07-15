---
layout: post3
title: Abstract Factory Pattern
comments: true
categories: [Design Pattern]
tags: [Abstract Factory]
toc: true
---
{:.no_toc}
## Contents

- TOC
 {:toc}
---

## What is Abstract Factory Pattern

> Abstract Factory Pattern provides an interface for creating combinations of objects that are correlated or dependent on each other without relying on concrete classes.

![CQ2](/public/images/AF3.PNG)

![CQ2](/public/images/AF4.PNG)

- AbstractFactory : The actual common interface of the class factory.
- ConcreteFactory : Override abstract methods of the AbstractFactory class to create concrete products.
- AbstractProduct : Common interface of product.
- ConcreteProduct : Concrete products created by concrete Factory class.

---

## Why use Abstract Factory Pattern?

The reason for using this pattern is to minimize the number of times a code is modified by reducing the degree of coupling with the client code by separating the code that creates the object.

#### `So, why does the degree of coupling decrease?`

It is because it used polymorphism, one of the object-oriented properties. Because the objects that make up the interface look at the same interface, they are flexible in the code.

#### `So, why is the number of code modifications minimized?`

Abstract Factory Pattern separates the creation of the object, so even if the object is added or modified, it only needs to modify the code that creates the object. First of all, creating an object is creating a concrete class, which is relatively likely to add or delete new objects. For example, suppose you have a syntax "if" or "else if" that creates objects within 10 classes. If an object is added or modified, it is necessary to change every classes. To solve these problems, we use `Abstract Factory Pattern`.

This pattern is useful in creating different types of objects that are related to each other in a consistent way.

---

If you look at factory method pattern, it looks similar to abstract factory pattern. And, there are several things in common between them.

### Abstract Factory and Factory Method in Common.

1. Use Template Method Pattern.
2. Create factory class.
3. Use Factory Method Pattern.
4. Encapsulate object creation.
5. Focuses on abstract classes and interfaces rather than concrete classes.
   - Both reduce the degree of coupling between the concrete class and client through abstract class and factory class.

`Abstract Factory Pattern` looks similar to `Factory Method Pattern`, but there's a difference.
Factory method pattern is a pattern in which the creation of objects based on conditions is delegated to the factory class, creating objects in the factory class.

---

### Difference

1. `Range to support creation of objects` in the Factory class
   - Abstract Factory Pattern : Multiple types of associated objects per factory (multiple create methods).
   - Factory Method Pattern : One type of object per factory (one create() method).
2. The `type of object` that the `factory method` creates.
   - Abstract Factory Pattern : The factor determines the type of factory that creates the related objects.
   - Factory Method Pattern : The type of object is determined by the factor.
3. Target to `lower the degree of coupling`.
   - Abstract Factory Pattern : Between ConcreteFactory and Clinet
   - Factory Method Pattern : Between ConcreteProduct and Client.

---

## Example

If we want to buy a `mechanical keyboard`, there are various switches such as cherry, gateron, membrane, and others. Also, keyboards have body and reinforcement plate as well as switch.
So, simply it can be said that the keyboard consists of `body`, `plate` and `switch`.

Now, imagine that this keyboard store only sell `Gateron` and `Cherry` products.

And, in this keyboard store, the gateron keyboard is made by using a plastic body, a plastic reinforced plate and blue gateron switches. The cherry keyboard is made by using a aluminum body, a aluminum plate, and red cherry switches.

- KeyboardStore
  - Cherry Keyboard
    - Body: Aluminum (Cherry Body)
    - Plate: Aluminum (Cherry Plate)
    - Switch: Red cherry switch (Cherry Switch)
  - Gateron keyboard
    - Body: Plastic (Gateron Body)
    - Plate: Plastic (Gateron Plate)
    - Switch: Blue gateron switch (Gateron Switch)

---

First, make an interface. `KeyboardsComponoentsFactory` provides common functionality to make body, plate, and switch.

```java
public interface KeyboardsComponentsFactory {

    public Body makeBody();

    // Reinforcement plate
    public Plate makePlate();

    public Switchtype makeSwitch();

}
```

---

Then, creates two classes that implements `KeyboardsComponentsFactory` interface.

`CherryComponentsFactory` produces aluminum body, aluminum plate, and red cherry switch for their product.

`GateronComponentsFactory` produces plastic body, plastic plate, and blue gateron switch for their product.

```java
public class CherryComponentsFactory implements KeyboardsComponentsFactory {
    @Override
    public Body makeBody() {
        return new CherryBody();
    }

    @Override
    public Plate makePlate() {
        return new CherryPlate();

    }

    @Override
    public Switchtype makeSwitch() {
        return new CherrySwitch();
    }
}

public class GateronComponentsFactory implements KeyboardsComponentsFactory {
    @Override
    public Body makeBody() {
        return new GateronBody();
    }

    @Override
    public Plate makePlate() {
        return new GateronPlate();

    }

    @Override
    public Switchtype makeSwitch() {
        return new GateronSwitch();
    }
}
```

---

Make interfaces for body, plate, and switch. Then, create classes that implement these components.

```java
// Interfaces for keyboard.
public interface Body {
    public String getName();
}

public interface Plate {
    public String getName();
}

public interface Switchtype {
    public String getName();
}

// Cherry Keyboard Components.
public class CherryBody implements Body {
    @Override
    public String getName() {
        return "Aluminium";
    }
}

public class CherryPlate implements Plate {
    @Override
    public String getName() {
        return "Aluminium";
    }
}

public class CherrySwitch implements Switchtype {
    @Override
    public String getName() {
        return "Red Cherry Switch";
    }
}

// Gateron Keyboard Components.
public class GateronBody implements Body {
    @Override
    public String getName() {
        return "Plastic";
    }
}

public class GateronPlate implements Plate {
    @Override
    public String getName() {
        return "Plastic";
    }
}

public class GateronSwitch implements Switchtype {
    @Override
    public String getName() {
        return "Blue Gateron Switch";
    }
}
```

---

Now, if you look at the abstract class `Keyboards`, you can assemble the keyboard with an abstract method called `assembling`.

```java
public abstract class Keyboards {
    String name;
    Body body;
    Plate plate;
    Switchtype switchtype;

    abstract void assembling();

    void prepare() {

        System.out.println("Preparing the assembled keyboard..");
    }

    void packing() {

        System.out.println("Packing the keyboard..");
    }

    public String getName() {

        return name;
    }

    public void setName(String name) {

        this.name = name;
    }
}
```

---

There are two keyboard classes that implement `Keyboards` interface. Using an instance of `KeyboardsComponentsFactory`, get the keyboard components directly and assemble the keyboard with the `assembling` method.

```java
public class CherryKeyboards extends Keyboards {
    KeyboardsComponentsFactory keyboardsComponentsFactory;

    public CherryKeyboards(KeyboardsComponentsFactory keyboardsComponentsFactory) {
        this.keyboardsComponentsFactory = keyboardsComponentsFactory;
    }

    @Override
    void assembling() {

        System.out.println("Making keyboard.. [" + name + "]");
        body = keyboardsComponentsFactory.makeBody();
        plate = keyboardsComponentsFactory.makePlate();
        switchtype = keyboardsComponentsFactory.makeSwitch();
        System.out.println("Keyboard Info : Body = [" + body.getName() + "], Plate = [" + plate.getName()
                + "], Switch Type = [" + switchtype.getName() + "].");
    }
}

public class GateronKeyboards extends Keyboards {
    KeyboardsComponentsFactory keyboardsComponentsFactory;

    public GateronKeyboards(KeyboardsComponentsFactory keyboardsComponentsFactory) {
        this.keyboardsComponentsFactory = keyboardsComponentsFactory;
    }

    @Override
    void assembling() {

        System.out.println("Making keyboard.. [" + name + "]");
        body = keyboardsComponentsFactory.makeBody();
        plate = keyboardsComponentsFactory.makePlate();
        switchtype = keyboardsComponentsFactory.makeSwitch();
        System.out.println("Keyboard Info : Body = [" + body.getName() + "], Plate = [" + plate.getName()
                + "], Switch Type = [" + switchtype.getName() + "].");

    }
}
```

---

Finally, we need to create a store called `KeyboardStore` where we can get orders from customers.

Set the VendorID such as `CHERRY` and `GATERON`. Then, a customer can order a cherry keyboard and gateron keyboard using `VendorID`.

```java
public enum VendorID {
    CHERRY, GATERON
}

public abstract class KeyboardStoreFactory {
    public Keyboards orderKeyboards(VendorID venderID) {
        Keyboards keyboard;

        keyboard = makeKeyboards(venderID);
        keyboard.assembling();
        keyboard.prepare();
        keyboard.packing();

        return keyboard;
    }

    abstract Keyboards makeKeyboards(VendorID venderID);
}

public class KeyboardStore extends KeyboardStoreFactory {
    @Override
    public Keyboards makeKeyboards(VendorID vendorID) {

        Keyboards keyboard = null;
        switch (vendorID) {
            case CHERRY:
                keyboard = new CherryKeyboards(new CherryComponentsFactory());
                keyboard.setName("Red Cherry Keyboard");
                break;

            case GATERON:
                keyboard = new GateronKeyboards(new GateronComponentsFactory());
                keyboard.setName("Blue Gateron Keyboard");
                break;
        }
        return keyboard;
    }
}
```

---

Let's test the pattern.

Thoruhg the `Client` class, the manufacturers will produce components of keyboard and assemble the keyboards based on the vendorID. If the customer orders a "Red Cherry Keyboard" from vendor `CHERRY`, the "Red Cherry Keyboard" will be delivered to customer.
If the customer orders a "Blue Gateron Keyboard" from vendor `GATERON`, the "Blue Gateron Keyboard" will be delivered to customer.

```java
public class Client {
    public static void main(String[] args) {

        KeyboardStore keyboardOrder01 = new KeyboardStore();

        VendorID vendorID;
        vendorID = VendorID.CHERRY;
        keyboardOrder01.orderKeyboards(vendorID);

        System.out.println();
        vendorID = VendorID.GATERON;
        keyboardOrder01.orderKeyboards(vendorID);
    }
}
```

![CQ2](/public/images/AF8.PNG)

---

### UML diagram

![CQ2](/public/images/AF9.PNG)

## Implementation

[Github](https://github.com/HyoSup0513/study/tree/master/Design%20Pattern/Abstract%20Factory%20Pattern)
