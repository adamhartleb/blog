---
title: 'C# Inheritance'
date: 2020-02-24T16:11:33-08:00
draft: true
tags: ['c#']
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

This will call the constructor in the parent class witht the value of `s`.
