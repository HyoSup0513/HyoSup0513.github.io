---
layout: post3
title: Builder Pattern
comments: true
categories: [Design Pattern]
tags: [Builder]
toc: true
---
{:.no_toc}
## Contents

- TOC
 {:toc}
---

## What is Builder Pattern?

> Builder design pattern separates the construction of a complex object from its representation so that the same construction process can create different representations.

![CQ2](/public/images/BP1.PNG)

- `AbstractClass` : Abstract interface for creating objects (product)
- `ConcreteClass` : The implementation class of the builder. A class that allows you to create other objects. Create and assemble parts to create objects.
- `Director` : Director class is responsible for the precise sequence of object creation. This class takes ConcreteBuilder as a parameter and performs the necessary actions.
- `Product` : Final objects created by Director using Builder.

---

## Why use Builder Pattern?

1. Encapsulates code for construction and representation.
2. Provides control over steps of construction process.
3. Create objects without creating unnecessary constructors.
4. Create objects regardless of the order of the data.

When creating an instance, it is difficult to create only through the `constructor`.

Assigning too many parameters to the constructor makes it difficult to determine which factor represents which value. In some instances, it may be necessary to create only a specific parameter. In this case, the value corresponding to a particular parameter must be passed to null, which is very bad in terms of the readability of the code.

```java
public Student(long cwid, String name, String major, int age, String email) {
this.cwid = cwid;
this.name = name;
this.major = major;
this.age = age;
this.email = email;
}
```

If we use this constructor to create an student instance.

It should be like this:

```java
Student student = new Student(888801234, "john", "CS", 22, "john1234@gmail.com");
```

But you may only know the student's ID and name. At this case, `the gargage data` or `null value` must be passed over to the constructor's parameter.

```java
Student student = new Student(888801234, "john", null, 0, null);
```

But, it is difficult to determine what value a particular parameter represents. This is why we use a builder pattern.

Instead of creating the required objects directly from the client, create the builder object by passing over the required parameters, and then call the defined methods on the builder object to create an instance.

---

### Problems

1. Adding object creation is easy, but adding new parts that construct an object is difficult.
2. Requires creating a separate `ConcreteBuilder` for each different type of product

---

## Example

### To implement Builder Pattern

1. First, Create the builder class as a `Static Nested Class`. Use the `Builder` keyword for the class you want to create. For example, the name of the student class for the Computer class is StudentBuilder.
2. The constructor of the builder class uses the `public` keyword. Essential parameters are passed over as paramerters of the constructor.
3. Use method for nonessential parameter. The return value of the method must be the builder object itself.
4. Finally, define a build() method within the builder class to provide object creation. And, it should use `private` keyword to create an object only through build().

---

Here, the Student class has only the `getter method` without the setter method, and there is no `public constructor`. Therefore, getting a Student object is only possible through the StudentBuilder class.
The `id` and `name` are essential parameters. And, others are optional parameters.

```java
public class Student {
    private long id;
    private String name;
    private String major;
    private int age;
    private String email;

    public Student() {
    }

    @Override
    public String toString() {
        return "Student [id]: " + id + " [name]: " + name + " [major]: " + major + " [age]: " + age + " [address]: "
                + email;
    }

    public static class StudentBuilder {
        // Essential parameter
        private final long id;
        private final String name;
        // Selective parameter
        private String major = "";
        private int age = 0;
        private String email = "";

        public StudentBuilder(long id, String name) {
            this.id = id;
            this.name = name;
        }

        public StudentBuilder major(String major) {
            this.major = major;
            return this;
        }

        public StudentBuilder age(int age) {
            this.age = age;
            return this;
        }

        public StudentBuilder email(String email) {
            this.email = email;
            return this;
        }

        public Student build() {
            return new Student(this);
        }
    }

    private Student(StudentBuilder builder) {
        this.id = builder.id;
        this.name = builder.name;
        this.major = builder.major;
        this.age = builder.age;
        this.email = builder.email;
    }
}
```

---

Let's use the StudentBuilder.

```java
public class Client {
    public static void main(String[] args) {
        Student s1 = new Student.StudentBuilder(888801234, "John").major("Computer Science").age(22)
                .email("john1234@gmail.com").build();
        System.out.println(s1);
    }
}
```

#### Output
![CQ2](/public/images/BP2.PNG)

You can create object like this. As you can see, the StudentBuilder class is used to create the Student object `s1`. 
`888801234` is `John`'s ID, and both parameters are essential. `major`, `age`, `email` are optional. Finally, `build()` creates and returns the object.

---

## Implementation

[Github](https://github.com/HyoSup0513/study/tree/master/Design%20Pattern/Builder%20Pattern)
