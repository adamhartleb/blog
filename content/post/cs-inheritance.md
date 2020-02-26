---
title: 'C# Inheritance'
date: 2020-02-24T16:11:33-08:00
draft: true
tags: ['csharp']
---

Inheritance is a way to reuse methods and properties in a class by creating a more specific class (termed _subclass_ or _derived class_) which then inherits from a base/parent class. A quintessential example is a base class called `Polygon`. Now all polygons have a certain number of sides which we can model:

```
class Polygon
{
    public int Sides { get; set; } = 0;

    public Polygon() {}

    public Polygon(int s) { Sides = s; }
}
```

Now a square is a type of polygon so it has a number of sides. Instead of creating a `Square` class with its own `Sides` field, we can create a `Square` class that **inherits** from the Polygon class which provides access to all the properties and methods defined on `Polygon`:

```
class Square : Polygon
{
    // Empty
}
```

We can then create an instance of `Square` and access the `Sides` property on it:

```
Square s = new Square();
s.Sides = 4;
Console.WriteLine(s.Sides);
```

Simply put: anything an instance of `Polygon` can do, an instance of `Square` can do too because a square **is** a polygon. We can confirm that via:

```
if (s is Polygon)
{
    Console.WriteLine("This is true");
}
```

Since a Square is a type of Polygon we can use that as our type when creating it the variable:

```
Polygon p = new Square();
```

The problem with this approach is that `s` does not have access to the fields and properties defined on the `Square` class because while all squares are polygons, not all polygons are squares. We can **cast** an instance of `Polygon` to a `Square` though using the `as` keyword:

```
Polygon p = new Square();
Square s = p as Square;
```

You cannot instantiate a subclass using the constructor from its parent class. However, when a subclass has a constructor, it **must** call the constructor in its parent class. For example:

```
class Square : Polygon
{
    public Square(int s) : base(s)
    {
        // Empty
    }
}
```

This will call the constructor in the parent class with the value of `s`.

### Protected

In addition to the `public` and `private` access modifiers, there is also the `protected` modifier. If a field uses the `protected` modifier then anything inside of that class **and also** any method in a subclass can access the field.

### object class

All classes always inherit from a root class called `object`. That means you can create any type in C# with the `object` type:

```
object s = new Square();
```

### Sealed

If you want to prevent a class from being inherited, you can declare it using the `sealed` keyword:

```
sealed class Square {}
```

### Partial

Class definitions can be split across multiple files for readability using the partial keyword:

```
// file A.cs
public partial class Square {}
```

```
// file B.cs
public partial class Square {}
```

You can also declare partial methods. It's a bit different than partial classes because there can only be one definition for a method, but you can define the method header in one partial class and the implementation in another. If you define the header for a method but never implement it, then any location in your code that calls the method will be removed by the compiler.

### Multiple Inheritance

Unlike languages like C++ and Python, C# does not support multiple inheritance so you can only ever inherit from one other class.
