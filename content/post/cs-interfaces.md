---
title: 'C# Interfaces'
date: 2020-02-26T19:40:26-08:00
draft: true
---

An interface defines a contract that specifies what methods a class must implement in order to satisfy that contract. Any class that implements an interface is guaranteed to have those methods or the code will not compile. Creating an interface is similar to creating a class or a struct:

```
public interface IFileReader {
  void Read(string filename);
}
```

As you probably notice, the interface does not implement the method, it only declares it. This is similar to how abstract classes work. So why use an interface if an abstract class will do or vice versa?

1. You can inherit from multiple interfaces, but you can only inherit from one class.

2. Abstract classes still allow you to implement methods while interfaces do not.

3. Abstract classes represent an "is-a" relationship so it's used for objects that are closely related. Interfaces represent a "can-do" relationship and is used for providing common functionality to unrelated classes.

To implement an interface, we use a colon like inheritance:

```
class Reader : IFileReader
{
  public string FileType { get; }

  public void Read(string filename)
  {
    // ...
  }
}
```

Similar to classes and structs, they can be treated as types so you can have an array of them:

```
IFileReader[] readers = new IFileReader[5];
```

Or you can accept them as an argument to a method:

```
public void doSomething(IFileReader r)
{
  // ...
}
```

To implement multiple interfaces, you just add a comma after the first:

```
class Reader : IFileReader, AnotherInterface, Interface3
{
  // ...
}
```
