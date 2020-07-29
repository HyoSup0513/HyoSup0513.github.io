---
layout: post3
title: State Pattern
comments: true
categories: [Design Pattern]
tags: [State]
toc: true
---
{:.no_toc}
## Contents

- TOC
 {:toc}
---

## What is State Pattern?

> State pattern that allows allows an object to alter its behavior when its internal state changes, so that the object looks like changing its class.

![CQ2](/public/images/SP1.PNG)

- `Context` : Defines the interface of interst to clients. Maintain and manage instances of the Concrete State subclass that defines the current state.
- `State`: Defines an interface to encapsulates the behavior associated with the state of the context.
- `Concrete State`: Each subclass implements a behavior associated with a state of the Context.

Each class declares the state of an object, and the class defines the behaviors that can be done in that state as a method. And encapsulates each of these state classes into an interface, calling the interface from the client.

It is `easy to add a new state` when the internal state of an object is likely to continue to be added. In addition, the behavior can be changed without changing the existing source code when changing the state of an object, including the added state.

---

## Why use State Pattern?

1. It is easy to change behavior according to changes in state.
2. Conditional statements may not be used.
3. It brings together behaviors related to a particular state into a single object.
4. The state transitions are explicit.

For example, when you use a computer, you can turn it on, turn it off, or turn on sleep mode.

- If the power button is pressed while the pc is `powered on`, the power should be `turned off`.
- If the power button is pressed while the pc is powered off, the power should be `turned on`.
- If the power button is pressed while the pc is in `sleep mode`, the power should be `turned on`.

```java
public class PC {
    public static String On = "on";
    public static String Off = "off";
    public static String Sleep = "sleep";
    private String powerState = "";

    public PC(){
        setPowerState(PC.Off);
    }

    public void setPowerState(String powerState){
        this.powerState = powerState;
    }

    public void pushPower(){
        if ("on".equals(this.powerState)) {
            System.out.println("Power off");
        }
        else if ("saving".equals(this.powerState)){
            System.out.println("Power on");
        }
        else {
            System.out.println("Sleep mode");
        }
    }
}
```

However, if we add the necessary states in this way, the conditional statement will be longer and longer. And, it won't be easy to understand what happens depending on the state. Also, if you want to change the function of the state when there are other electronic devices as well as `PC`, you have to change everything.

So the pattern that you use when it needs to behave differently depending on the state is a `state pattern`.

---

## Problems

- The number of classes required increases.

Therefore, it is important to consider whether there is a possibility that more types of states are being added. It should be looked at whether there is a need to manage the behaviors that need to be carried out under certain states.

---

## Example

Each `on`, `off`, and `sleep` state is defined using the class and grouped into one interface `PowerState`.
Then when a PC calls a method in the `PowerState` interface, the defined behavior is performed on each state class.

---

First, declare an interface encapsulating the power state. Next, define each state class that implements the `PowerState` interface.

```java
public interface PowerState {
    public void pushPower();
}

public class OffState implements PowerState {
    public void pushPower() {
        System.out.println("Power off");
    }
}

public class OnState implements PowerState {

    @Override
    public void pushPower() {
        System.out.println("Power on");
    }
}

public class SleepState implements PowerState {
    public void pushPower() {
        System.out.println("Sleep mode");
    }
}
```

---

Declares a `PC` class and sets the existing state to `off`. Then call the `pushPower` of the interface.

```java
public class PC {
    private PowerState powerState;

    public PC() {
        this.powerState = new OffState();
    }

    public void setPowerState(PowerState powerState) {
        this.powerState = powerState;
    }

    public void pushPower() {
        powerState.pushPower();
    }
}
```

---

Define a `Client` class that use pc object. Let's test the pattern.

```java
public class Client {
    public static void main(String[] args) {
        PC pc = new PC();

        pc.pushPower();
        pc.setPowerState(new OnState());
        pc.pushPower();
        pc.setPowerState(new SleepState());
        pc.pushPower();
        pc.setPowerState(new OffState());
        pc.pushPower();
    }
}
```

#### Output

![CQ2](/public/images/SP3.PNG)

---

## Implementation

[Github](https://github.com/HyoSup0513/study/tree/master/Design%20Pattern/State%20Pattern)
