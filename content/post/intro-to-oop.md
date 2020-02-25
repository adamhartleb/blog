---
title: 'Intro to Object Oriented Programming'
date: 2020-02-21T15:07:11-08:00
draft: false
tags: ['oop', 'intro']
---

### Introduction

What exactly is an object? An object is defined by two components: properties and behaviors. A car has properties like its color, the year it was made, if it's 4WD or not, etc. It also has behaviors such as starting, driving and so on. Having both of these components is key because if you just have behaviors then you're simply dealing with functions that transform their inputs and return the output. If you only have properties then that's just a structure.

What's wrong with that though? If the components are separated then access to the properties is unrestricted. You could have multiple functions that access and mutate your data. Can you remember if that function you ran before mutated one of those properties? The fewer things we have to keep in mind, the fewer mistakes we potentially make.

Objects remedy this by combining the two components and controlling access to them. In object-oriented terminology, this is known as **encapsulation**. By defining methods and properties as restricted, another logically separate function cannot come in and modify the state of our object, only the object itself can do that. But then how do two objects communicate with eachother if access to their data is restricted? This is achieved through messaging which effectively means calling the other object's methods to return the desired value. The beauty of this approach is that `ObjA` doesn't need to know or care how `ObjB` calculated its result and coversely, `ObjB` can change how it derives the value without making changes to `ObjA`.

To illustrate the point, the car example above provides an interface through its steering wheel and pedals. When you press down on the gas pedal, the car accelerates, but you have no idea (for argument's sake) how it generated the power to do that. Knowing how the acceleration was generated is not your responsibility nor is it necessary to obtain the desired result.

### What is a Class?

How are objects created? They are created using classes. A class defines the properties and behaviors that all objects constructed from this class will have. In other words, a class is a blueprint for an object. Think of it like a blueprint for building a house. With a single blueprint, you can construct the same house (object) multiple times and each house will have its own copy of each feature. That list bit is important because these houses are not interconnected. For example, destroying a wall in one house does not result in the destruction of that wall in every house.

### The Four Pillars of OOP

The first pillar is Encapsulation. As previously mentioned, one of the primary benefits of objects is that they encapsulate and restrict access to their properties and behaviors. An object should only reveal a limited interface which defines the means of communication between it and another object. In most object-oriented languages, that entails declaring certain properties and methods with the `public` access level modifier. Members of the class declared `public` can be interacted with freely by another object. On the other hand, to hide data, members of the class are declared with the `private` modifier. Private members can only be accessed by public methods also defined on that class. Formally, this is achieved by public methods termed `getters` and `setters`.

The second pillar is Inheritance. Inheritance allows one class to inherit the properties and methods of another class. One of the most prevelant design problems in OOP is factoring out common functionality among classes. For example, suppose you have a `Manager` and `Employee` class and each has a common property called `name`. This property can be moved up to another class called `Person` from which `Manager` and `Employee` inherit. When a `Manager` or `Employee` object is instantiated, it will contain everything declared in its own class as well as everything from its parent class.

The third pillar is Abstraction. Our objects often don't represent the original real-world objects with 100% accuracy. Instead, we try to model specific properties and behaviors while ignoring the rest. For example, a `Remote` class would likely exist for a TV and an Air Conditioning app. The `Remote` for the TV would contain details related to controlling volume, channels, pictures, power etc, while for the AC it might contain only power and temperature. Here we're modeling a real-world object (the remote) for applications and each contains only the relevant details for their specific contexts.

The final pillar is Polymorphism. In Greek, Poly- means "many" while morph means "forms" so it literally translates to "many forms". Say we have `Dog`, `Cat` and `Bird` classes which all inherit from an `Animal` class. Each animal makes a specifc sound so each subclass has its own method for producing that sound. After instantaing our subclasses, we place each object in a bag labeled "Animals", mix them up, and create a program to pull them out one-by-one. Our program pulls out an animal, tells it to make a sound and the specific implementation of that animal invokes its sound method. Our program does not know at the time what it's pulling out, it just knows it can make a sound and the implementation carries out the rest.
