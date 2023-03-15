# Abstract Classes

## Learning Goals

- Explain abstract classes
- Create abstract classes

## Introduction

The classes that we have seen so far have had 3 basic properties:

1. They had variables (i.e. things that they are or that they have).
2. They had methods (i.e. things that they can do).
3. They could be instantiated (i.e. we could create variables based on them).

Now what if we wanted to have a base class, but didn't want anyone to be able
to instantiate it? Consider an `Animal` base class. One could imagine
that although all animals have some things and behaviors in common, some things
or behaviors are specific to an actual type of animal. Consider the sound that
an animal makes - there is no "generic" sound that is applicable to all animals.
So if we wanted to give all our animals the ability to make a sound, but we
couldn't implement a "generic" sound on the parent class, then we could make the
`Animal` class `abstract`.

In this lesson, we will define an abstract class `Animal` that will
be extended by a concrete class `Cat`. We italicize the names of abstract classes and abstract methods in the UML class diagram
as shown below.  Concrete class and methods are not italicized.

![abstract class uml](https://curriculum-content.s3.amazonaws.com/6677/pillars/abstract_class_uml.png)



## Abstract Class in Java

- An `abstract` class is a class that cannot be instantiated. 
- An abstract class may define one or more abstract methods.
- A class that extends an abstract class must override and implement all abstract methods, or must be
  declared abstract as well.

Let's consider the `Animal` class. 

- Concrete method `eat()`. 
  - We want all animals to eat.  The default implementation of the `eat()` method is to say "Yum! I like to eat!".
- Abstract method `makeSound()`.
  - We want all animals to be able to make a sound.
  - We do not think there is a generic sound that applies to all animals, so we
    don't want the `Animal` class to implement the `makeSound()` method. 

A class that defines an abstract method must be declared as abstract.
Let's add the keyword `abstract` to the class definition:

```java
public abstract class Animal {
    // ...
}
```

Then let's add an abstract method named `makeSound`:

```java
public abstract void makeSound();
```

An `abstract` method definition differs from a regular method in 2 ways:

1. It has the `abstract` keyword in its definition
2. It does not have any implementation code, so its signature is simply followed
   by a `;` to end the method definition

The abstract `Animal` class  is thus defined with a concrete method `eat()` and
an abstract method `makeSound()`:

```java
public abstract class Animal {

   public void eat() {
      System.out.println("Yum! I like to eat!");
   }

   public abstract void makeSound();
}
```

There is a 3rd difference that isn't evident from the method definition, but
that we mentioned before: an abstract class cannot be instantiated, so the
following statement would not compile:

```java
Animal baseAnimal = new Animal();
```

Essentially, the `Animal` class has now declared that it's "incomplete". It
wants to "make a sound", but it has not defined "how to make a sound", i.e. that
method has no implementation.



In order to be used, an `abstract` class must be extended and its `abstract`
methods must be implemented. For example, we can implement the `makeSound()`
method in a `Cat` class as follows:

```java
public class Cat extends Animal {
    
    public void useLitter() {
        System.out.println("I just used the litter - I'm a clean cat!");
    }
    
    @Override
    public void makeSound() {
        System.out.println("Meow");
    }
}
```
 
The `Cat` class can now be instantiated and used like before, including its
`makeSound()` method:

```java
Cat myCat = new Cat();
myCat.eat();         //concrete method inherited from Animal
myCat.useLitter();   //concrete method implemented in Cat
myCat.makeSound();   //abstract method overriden and implemented in Cat
```

As we can see, the `Animal` class has default behavior that applies to all
animals, like the `eat()` method.


Abstract classes are used when default properties and behaviors need to be
defined for a specific type of object, but some behavior needs to be left
undefined by the parent class and must be implemented by the child classes. In
this example, that behavior was the ability to make a sound.

We might be thinking that an alternative to adding the `abstract makeSound()`
method in the `Animal` class could have been to not add the method at all and
let each child class add their own implementation. The problem with that
approach is that each child class could decide for itself whether to have a
`makeSound()` method. Whereas what we want is to force all animals to have a
`makeSound()` method, without providing a base implementation for it.

We also want to establish that any `Animal` that doesn't make a sound is
"incomplete" and therefore cannot be used. So the `Animal` class cannot be
instantiated on its own and needs a subclass that implements the missing
functionality.

