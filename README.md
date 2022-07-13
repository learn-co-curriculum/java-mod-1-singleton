# Singleton

## Learning Goals

- Explain the singleton pattern
- Use the single pattern in Java

## Introduction

Use the singleton pattern when you need to control the number of instances
(usually to just one) of a specific class in your entire system. Here are the
highlights of the singleton pattern:

- Should be used when only one instance of a class should be created
- Use instead of static methods because the `getInstance()` method can control
  how many instances should be created and the single instance is better suited
  for managing data that should be shared across the entire system
- Where does it apply: a global resource in a system, like an application window
  manager, a file explore or a database driver

## Implementation

The Singleton pattern can be tricky to implement because additional precautions
must be taken in order to ensure that it performs properly in "multi-threaded"
environment. A "thread" is an abstraction the JVM provides to represent unit of
execution of your program. Java supports the ability to create many such units
so that your program can run multiple things at once, in which case resources
such as singletons may be shared across multiple units of execution. This will
be discussed in detail in another section. For now, our implementation of the
singleton pattern will be "naive" and will not worry about a multi-threaded
environment.

The general pattern for implementing a singleton is as follows:

1. A class, let's call it `SingletonClass`
2. A private constructor, so that the singleton class can never be created with
   the `new` keyword, like regular classes can
3. A private static member variable of the type `SingletonClass` that will be
   the only instance of `SingletonClass` ever created
4. A `static`, `public` method, let's call it `getInstance()`, that either
   returns the existing single instance of the class or creates the single
   instance if it hasn't already been created and then returns it

A generic singleton class would therefore look like this:

```java
public class SingletonClass {
    private static SingletonClass singleton;

    private SingletonClass() {
    }

    public static SingletonClass getInstance() {
        if (singleton == null) {
            singleton = new SingletonClass();
        }
        return singleton;
    }
}
```

Note that with this implementation, we could always modify the `getInstance()`
method at a later time if we wanted to have more than one instance of the
`SingletonClass`. Clients of this class would still just call `getInstance()` to
get an instance and continue to use it the same way.
