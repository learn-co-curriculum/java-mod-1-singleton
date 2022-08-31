# Singleton

## Learning Goals

- Explain the singleton pattern
- Use the single pattern in Java

## Introduction

A **singleton** is a creational design pattern that ensures only one instance
of the class exists within a system to provide a global access point. So what
does this mean and why should we implement it?

Think of a country as a system and a singleton as a government for a minute. If
the country were to have more than one government, it could result in chaos
with different governments conflicting. It is easier to just have one and let
that government be the one that is globally accepted. The same goes for a
singleton within a system. Perhaps we only want one instance of this class to
be used to control access to a shared resource. This is where a singleton
design pattern could be useful!

Here are the highlights of the singleton pattern:

- Should be used when we only want one instance of a class to be created.
- Use when a single instance is better suited for managing data that should be
  shared across the entire system.
- Apply the design pattern to a global resource in a system; like an application
  window manager, a file explore or a database driver.

## Implementation

The Singleton pattern can be tricky to implement because additional precautions
must be taken in order to ensure that it performs properly in a multithreaded
environment. We will learn more about multithreading and what exactly that means
in a later module, so we don't need to concern ourselves with the details on
that topic right now. For the time being, our implementation of the singleton
pattern will be "naive" and will not worry about a multithreaded environment.

The general pattern for implementing a singleton is as follows:

1. A class, let's call it `SingletonClass`.
2. A private constructor, so that the singleton class can never be created with
   the `new` keyword, like regular classes can.
3. A private static member variable of the type `SingletonClass` that will be
   the only instance of `SingletonClass` ever created.
4. A `static`, `public` method, let's call it `getInstance()`, that either
   returns the existing single instance of the class or creates the single
   instance if it hasn't already been created and then returns it.

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

## Example of a Singleton in Application

Let's see give a more concrete example of a singleton design pattern:

```java
class Database {
    /* Create a private static instance variable
       to be used in the getInstance() method */
    private static Database database;
    
    private Database() {
        /* Create a private constructor so 
           others cannot create it with the
           new keyword  */
    }
    
    public static Database getInstance() {
        
        /* Create the instance if and only if
           it has not been created yet */
        if (database == null) {
            database = new Database();
        }
        
        // Return the singleton object for use
        return database;
    }
    
    // Singletons can define business logic
    public void getConnection() {
        System.out.println("You are connected to the database.");
    }
}
```

The above code is an example of an applicable singleton design pattern. When we
connect to a database, we only really want to connect to it once. Therefore, a
singleton pattern is perfect to control that there is only one instance of a
database connection open! We will learn more about databases later, but know
that this is a more concrete example of how to implement the singleton design
pattern.
