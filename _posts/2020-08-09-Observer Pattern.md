---
layout: post3
title: Observer Pattern
comments: true
categories: [Design Pattern]
tags: [Observer]
toc: true
---
{:.no_toc}
## Contents

- TOC
 {:toc}
---

## What is Observer Pattern?

> Observer pattern a design pattern that an object (subject) maintains a list of its dependents (observers), and notifies them automatically of any state changes, usually by calling one of their methods.

![CQ2](/public/images/OP01.PNG)

- `Observer` : Interface that is notified of changes in data. `Subject` notifies `ConcreteObserver` of the data change of the `ConcreteSubject` by invoking the update method of the `Observer` interface.
- `Subject` : Manage the ConcreteObserver object. Manages `ConcreteObserver` by referring to the Observer interface,so it can be independent of the change in `ConcreteObserver`.
- `ConcreteSubject`: A class with data that is subject to change management.
- `ConcreteObserver`: A class that is notified of the change in the ConcreteSubject. Changes are notified by implementing the update method of the Observer interface.

Observer pattern constructs a one-to-many object dependency relationship so that the state of another object is also linked with the state change of one object.

This means that when an object's state changes, it becomes possible to notify the related objects of the change in state without relying on a particular object.

This pattern is also called the `Pub/Sub` model.

---

## Why use Observer Pattern?

1. It is useful when you want to notify a data change without relying on a relative class or object when it occurs.
2. The degree of coupling between the subject class and the Observer class is low.
3. Because the subject class and the Observer class are independent of each other, the two classes can be changed and reused independently of each other.

For example, if you use YouTube, there are various channels and you can subscribe to them. In this example, the YouTube channel becomes the `publisher` and people who subscribed the channel becomes the `subscriber` (Observer). If a YouTuber uploads a new video, subscribers can be notified that the video has been uploaded. So each user will be an observer who is subscribing to the YouTube channel.

---

If we use `Discord`, there is one server and we can chat on that server.

```java
public class User {
    private Server server;

    public void setRoom(Server server){
        this.server = server;
    }

    public void chat(String message){
        room.receive(message);
    }
}

public class Server {
    public void receive(String message){
        System.out.println(message);
    }
}

public class Client {
    public static void main(String args[]){
        User user = new User();
        Server server = new Server();

        user.setServer(room);

        String message = "Thank you!";
        user.chat(message);
    }
}
```

---

However, there can be many servers, and users can enter them.
Imagine if the user is the owner of the server and should notify the server they manage. Then, when the manager chatted, the message should be delivered to all chat servers.

```java
import java.util.List;

public class User {
    private List<DiscordServer> server;

    public void setServer(List<DiscordServer> server) {
        this.server = server;
    }

    public void send(String message) {
        for (DiscordServer s : server) {
            s.receive(message);
        }
    }
}

public class DiscordServer {
    public String serverTitle;

    public void receive(String message) {
        System.out.println("Received message from server " + this.serverTitle + " : " + message);
    }
}

public class ServerA extends DiscordServer {
    public ServerA(String serverTitle) {
        this.serverTitle = serverTitle;
    }
}

public class ServerB extends DiscordServer {
    public ServerB(String serverTitle) {
        this.serverTitle = serverTitle;
    }
}

public class ServerC extends DiscordServer {
    public ServerC(String serverTitle) {
        this.serverTitle = serverTitle;
    }
}

import java.util.ArrayList;
import java.util.List;

public class Client {

    public static void main(String[] args) {
        User user = new User();
        List<DiscordServer> server = new ArrayList<DiscordServer>();
        server.add(new ServerA("[Discuss Server]"));
        server.add(new ServerB("[Game Server]"));
        server.add(new ServerC("[Development Server]"));

        user.setServer(server);

        String message = "Please follow the chatting rules. !";
        user.send(message);
    }
}
```

Define three server `ServerA`, `ServerB`, and `ServerC` classes and encapsulate them into the `Server` class.
But, the user and server are connected very strongly in the client. What if a new server should be created or removed?

At this time, the use of the Observer pattern makes the system flexible and eliminates object-to-object dependencies.

---

## Problems

- Observer objects can change the information of the subject objects to one another, which can cause the same change to be repeated by different objects. This is because the Subject objects and the Observer objects only exchange the fact that the data values have changed. Therefore, to prevent this, it is necessary to explicitly exchange what data values have been changed.

---

## Example

#### Server Structure

- Discord Server
  - ServerA
  - ServerB
  - ServerC

---

First, make `ServerA`, `ServerB`, `ServerC` as an observer.
To do that, we will define the observer class and encapsulate the servers.

The Observer can be defined as an interface, but we will use class here.

```java
public class Observer {
    public String serverTitle;

    public void receive(String message) {
        System.out.println("[" + this.serverTitle + "] " + "has received message : " + message);
    }
}

public class ServerA extends Observer {
    public ServerA(String serverTitle) {
        this.serverTitle = serverTitle;
    }
}

public class ServerB extends Observer {
    public ServerB(String serverTitle) {
        this.serverTitle = serverTitle;
    }
}

public class ServerC extends Observer {
    public ServerC(String serverTitle) {
        this.serverTitle = serverTitle;
    }
}
```

---

Next, define the `Subject` class that defines attach, detach, and notify. Then make the User class inherit the Subject class.
Therefore, the `User` class will be able to manage the Observers.

```java
import java.util.ArrayList;
import java.util.List;

public class Subject {
    private List<Observer> observers = new ArrayList<Observer>();

    // Add to Observer
    public void attach(Observer observer) {
        observers.add(observer);
    }

    // Remove from Observer
    public void detach(Observer observer) {
        observers.remove(observer);
    }

    // Notify the Observer
    public void notifyObservers(String message) {
        for (Observer o : observers) {
            o.receive(message);
        }
    }
}

public class User extends Subject{

}
```

---

Finally, let's test the pattern in `Client`. Also, you can see a decrease in dependence in the `Client`, unlike before.

```java
public class Client {
    public static void main(String[] args) {
        User user = new User();
        ServerA discuss = new ServerA("Discuss server");
        ServerB game = new ServerB("Game server");
        ServerC dev = new ServerC("Development server");
        user.attach(discuss);
        user.attach(game);
        user.attach(dev);

        String message = "Please follow the chatting rules !";
        user.notifyObservers(message);

        user.detach(discuss);
        user.detach(dev);
        message = "Manner maketh the man !";
        user.notifyObservers(message);
    }
}
```

---

#### Output

![CQ2](/public/images/OP02.PNG)

---

## Implementation

[Github](https://github.com/HyoSup0513/study/tree/master/Design%20Pattern/Observer%20Pattern)
