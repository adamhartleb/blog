---
title: 'C# Generics'
date: 2020-03-01
draft: false
tags: ['csharp']
---

Imagine that you created a method that accepts an array of numbers and loops over them and writes the value at each index to the console. Now imagine you wanted similar functionality, but applied to an array of doubles, strings or booleans. Now, you can't use your original method because it only accepts numbers so you have two alterntives:

1. You could create a method that does the same thing for each type.
2. You could use the `object` type instead of each specific subtype.

The problem with #1 is that it results in code duplication. If you want to make a change to how each method logs their value, you'll have to apply the change to each method separately. The issue with #2 is that you now need to cast each `object` type to the specific subtype in order to actually do anything with it or the code own't be type safe. Casting is an expensive operation and it makes your code harder to read.

In comes `generics`. Generics provide a way to define type safe classes without having to commit to one specific type. The built-in `List` class is an example of a generic class. It provides similar functionality to an array except that it can grow and shrink. Here's how you can create an instance of List:

```
using System.Collections.Generic;

List<int> listOfNums = new List<int>();
```

The angle brackets `<` and `>` hold what is called a **generic type parameter**. Now if you want to add a number to the list:

```
listOfNums.Add(3);
```

Since we've specified a generic type parameter of `int`, the Add method expects us to provide an int.

Another example of a generic is the `Dictionary` class. A dictionary is a key-value store. If you open an actual dictionary, you can flip to a word and see its definition. Similarly, a Dictionary in C# has a key (the word) and a value associated with it (the definition). The keys and values don't have to be strings, they can be generic types. Here's how you would create a dictionary:

```
Dictionary<string, string> myDictionary = new Dictionary<string, string>();
```

In the generic type parameters above `<string, string>` the first string is for the type of the key and the second is for the type of the value. To add to the dictionary, we can write:

```
myDictionary["someKey"] = "here is a value";
```

Similarly, to retrieve a value:

```
string myValue = myDictionary["someKey"];
```

### Creating Generics

We can also create our own generic classes. Here's an example:

```
public class MyGeneric<T>
{
    // ...
}
```

Here we have another generic type parameter attached to the name of the class. The `<T>` is the placeholder for our generic type, but it doesn't have to be the letter "T". Now we can use that type in our class:

```
public class MyGeneric<T>
{
    private T[] myArray;

    public MyGeneric()
    {
        myArray = new T[3];
    }

    public void AddValue(int index, T value)
    {
        myArray[index] = value;
    }

    public T GetValue(int index)
    {
        return myArray[index];
    }
}

class Program
{
    static void Main(string[] args)
    {
        var v = new MyGeneric<int>();
        v.AddValue(0, 4);
        Console.WriteLine(v.GetValue(0));
    }
}
```

There is still the elephant in the room though. My class can accept a generic type, but we still don't have any idea what type that will be so how can we know what methods are available? You can constrain the generic type to one that implements a specific interface:

```
public class MyGeneric<T> where T : ISomeInterface
{
    // ...
}
```

In addition to classes, methods can be generic as depicted in our opening example.

```
public T MyMethod<T>(T someArg)
{
    // ...
}
```
