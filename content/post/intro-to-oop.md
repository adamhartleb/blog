---
title: 'Intro to OOP'
date: 2020-02-21T15:07:11-08:00
draft: true
---

### Introduction

What exactly is an object? An object is defined by two components: properties and behaviors. A car has properties like its color, the year it was made, if it's 4WD or not, etc. It also has behaviors such as starting, driving and so on. Having both of these components is key because if you just have behaviors then you're simply dealing with functions that transform their inputs and return the output. If you only have properties then that's just a structure.

What's wrong with that though? If the components are separated then access to the properties is unrestricted. You could have multiple functions that access and mutate your data. Can you remember if that function you ran before mutated one of those properties? The fewer things we have to keep in mind, the fewer mistakes we potentially make.

Objects remedy this by combining the two components and controlling access to them. In object-oriented terminology, this is known as **encapsulation**. By defining methods and properties as restricted, another logically separate function cannot come in and modify the state of our object, only the object itself can do that. But then how do two objects communicate with eachother if access to their data is restricted? This is achieved through messaging which effectively means calling the other object's methods to return the desired value. The beauty of this approach is that `ObjA` doesn't need to know or care how `ObjB` calculated its result and coversely, `ObjB` can change how it derives the value without making changes to `ObjA`.

To illustrate the point, the car mentioned above provides an interface through its steering wheel and pedals. When you press down on the gas pedal, the car accelerates, but you have no idea (for argument's sake) how it generated the power to do that. Knowing how the acceleration was generated is not your responsibility nor is it necessary to obtain the desired result.

### What is a Class?

How are objects created? They are created using classes. A class defines the properties and behaviors that all objects constructed from this class will have. In other words, a class is a blueprint for an object. Think of it like a blueprint for building a house. With a single blueprint, you can construct the same house (object) multiple times and each house will have its own copy of each feature. That list bit is important because these houses are not interconnected. For example, destroying a wall in one house does not result in the destruction of that wall in every house.
