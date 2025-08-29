---
title: Dependency Injection - A Core Concept
published: true
---

If we've ever chatted about software design, you've likely heard me rave about Dependency Injection (DI). For those who haven't, I am here to share the lore.

Dependency Injection in its raw form is a design pattern that focuses on delivering a class or function its dependencies from the outside, instead of letting it create them on its own. 

So, what exactly is a `dependency`? It is something a software program needs to do its job. We can see this in two primary contexts:

**Object Dependencies:**

In object-oriented programming, a class often relies on other classes to function. These are its object dependencies. The goal of DI is to provide these dependencies to the object when it is created/instantiated.

For example, in a Java program, an `Adder` class might need two numbers to perform its calculation. Instead of creating those numbers internally, we can design the class to receive them through its constructor.

```java
public class Adder {
    // These are the class dependencies (member variables)
    private int number1;
    private int number2;

    // The constructor is used to "inject" the dependencies
    public Adder(int number1, int number2) {
        this.number1 = number1;
        this.number2 = number2;
    }
}
```

In this case, `number1` and `number2` are dependencies of the `Adder` object because the object cannot be instantiated without them being "injected" through its constructor.

**Function Dependencies:**

In functional programming, a function's dependencies are its parameters. The function is designed to be pure, meaning its output is determined solely by the inputs it receives.
For example, in Kotlin, the `addTwoNumbers` function depends on `number1` and `number2` to perform its calculation.

```java
fun addTwoNumbers(number1: Int, number2: Int): Int {
    return number1 + number2
}
```

The function cannot be executed without these two numbers being passed in as a function call.

The patterns used to deliver a program's dependencies, as shown above, largely affect its modularity and composability. I've come to learn that well-designed systems with dependency injection are made up of loosely coupled parts that are easy to test and maintain.

This feels like a good place to pause. We've explored dependencies in a software program's context. While writing this, I gained even more clarity on the different ways dependencies are delivered, the single-threaded and single-process nature of DI patterns, and even runtime vs. compile-time considerations for DI frameworks.

I might explore these topics in a later post. I should. :)