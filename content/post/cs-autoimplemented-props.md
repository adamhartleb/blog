+++
title = "C# Autoimplemented Properties"
description = "Learn how C#'s autoimplemented properties work."
date = 2020-02-19
author = "Adam Hartleb"
tags = ["csharp"]
+++

In object-oriented programming, you'll often be creating getters and setters for instance variables. For example:

```
class Book
{
  private string title;

  public Book(string title)
  {
    this.title = title;
  }

  GetTitle()
  {
    return title;
  }

  SetTitle(string title)
  {
    this.title = title;
  }
}
```

The problem with this is that it's verbose and creating getters and setters is extremely common so it becomes a little cumbersome. Now, you might be thinking "If I can just freely get and set the instance variable, why not make its accessibility public?" The issue with that approach is if you later decide to change how the variable is retrieved or set (e.g. we might want to check if the new title is not an empty string) then you risk breaking the interface that your code originally relied on.

A more concise way of dealing with this problem is to use **properties**:

```
class Book
{
  private string title;

  public Book(string title)
  {
    this.title = title;
  }

  public string Title
  {
    get
    {
      return title;
    }
    set
    {
      title = value;
    }
  }
}
```

And now we can access the `title` variable through the `Title` property:

```
var b = new Book("Name of the Wind");
Console.WriteLine(b.Title);

b.Title = "A Wise Man's Fear";
Console.WriteLine(b.Title);
```

When we access the `Title` property, the `get` block is executed. When we assign to the `Title` property the `set` block is executed and is implicitly passed the value we are assigning to a variable called `value`; this is similar to how `this` is implicitly passed into methods and refers to the instance of that class.

This pattern is still so common that an even shorter way is provided:

```
class Book
{
  private string title;

  public Book(string title)
  {
    this.title = title;
  }

  public string Title { get; set; }
}
```

However, with this approach, you no longer have access to the backing field which originally used to be `title`. Here, setting the `Title` property will not change the value of `title`. The value behind `Title` is effectively invisible.

If you wanted a **read-only** autoimplemented property, you can achieve that by dropping the set block:

```
class Book
{
  public string Title { get; }

  public Book(string title)
  {
    Title = title;
  }
}
```

For more information, [click here.](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/auto-implemented-properties)
