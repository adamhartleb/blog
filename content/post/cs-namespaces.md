---
title: 'C# Namespaces'
date: 2020-03-04
draft: false
---

In large programs or if you're using third-party libraries, you'll often encounter types with the same name as your own. In order to avoid such naming collisions, you can `namespace` your types. A namespace is simply a grouping of related code under a single name.

In our previous articles on C#, you'll notice we used:

```
using System;

Console.WriteLine("Hello");
```

However, this isn't the fully qualified name for the `WriteLine` method. The full name is `System.Console.WriteLine`. The `System` part is the namespace while the `Console` part is the class; altogether they form the fully qualified name for the method. For the sake of brevity though, we included the `using` directive. The directive allows us to import all of the names from a namespace into our file so we can just reference the name of the class without the namespace to access its methods.

Namespaces help prevent naming collisions, but they don't completely solve it. You could add two using directives for namespaces that define the same name for some types and encounter a naming collision. To fix that we can use an **alias**.

```
using WinformTimer = System.Windows.Forms.Timer;
using ThreadingTimer = System.Threading.Timer;
```

If the class you're referring to is `static`, you can use a static directive to not have to type the name of the class as well:

```
using static System.Console;

WriteLine("Hey!");
```
