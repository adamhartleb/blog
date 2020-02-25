+++
title = "C# Structs"
description = "Notes on structs in C#"
date = 2020-02-20
author = "Adam Hartleb"
tags = ["c#"]
+++

Structs and Classes are constructed very similarly in C#:

```
struct Book
{
    private string title;
    private int[] editions;
    public string Title
    {
        get { return title; }
        set { title = value; }
    }
    public string Author { get; set; }
    public int[] Editions
    {
        get { return editions; }
        set { editions = value; }
    }

    public string Blurb()
    {
        return $"{Title} by {Author}";
    }
}
```

And they are instantiated in the same way:

```
var b = new Book();
b.Title = "Name of the Wind";
b.Author = "Patrik Rothfuss";
Console.WriteLine(b.Blurb()); // outputs "Name of the Wind by Patrik Rothfuss"
```

They're so similar, you could simply change the "struct" keyword used above to "class" and you'll have a class instead. So what exactly is the difference between a struct and class then? The most important distinction is that classes are **reference** types while structs are **value** types. That means when a struct passes a method boundary (whether it's passed in as an argument or returned), its value is _copied_. For example:

```
static void Main(string[] args)
{
    var b = new Book();
    b.Title = "Name of the Wind";
    b.Author = "Patrik Rothfuss";
    Console.WriteLine(b.Blurb()); // outputs "Name of the Wind by Patrik Rothfuss"
    ChangeTitle(b);
    Console.WriteLine(b.Blurb()); // still outputs "Name of the Wind by Patrik Rothfuss"
}

static void ChangeTitle(Book b)
{
    b.Title = "Something Else";
}
```

As we can see, the value of the `title` field is not changed whereas if we used a class, the value would be changed.

There is a caveat though. If our struct contains a field that is a reference type, mutating the reference will change the field in both the copied struct and the original struct. We can see that here:

```
static void Main(string[] args)
{
    var b = new Book();
    b.Editions = new int[] { 1, 2, 3 };
    Console.WriteLine(b.Editions[0]); // outputs 1
    ChangeEdition(b);
    Console.WriteLine(b.Editions[0]); // outputs 9
}

static void ChangeEdition(Book b)
{
    b.Editions[0] = 9;
}
```

Some other differences between structs and classes include:

1. Since structs are value types they cannot be assigned `null` like a class.

2. Since structs are value types they are placed on the stack and not the heap.

3. Structs cannot have a parameterless constructor.

4. Structs cannot inherit like classes.

So when should you choose a class or a struct? Most of the time it depends if you need value or reference semantics. Structs are great if you just need to store a collection of primitive values.
