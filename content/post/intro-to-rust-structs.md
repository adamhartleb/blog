---
title: 'Intro to Rust - Structs'
date: 2020-03-03
draft: false
tags: ['rust', 'intro']
---

A struct is a data type that allows you to group multiple related values under a single type. To define a struct in Rust, we use the `struct` keyword:

```
struct Point {
    x: i32,
    y: i32,
}
```

And we create an instance of the struct like so:

```
let p = Point{ x: 3, y: 4 };
```

And to access a field on the struct we use dot notation:

```
println!("x: {}, y: {}", p.x, p.y);
```

If you wanted to change the value of a field, you could write:

```
p.x = 18;
```

However, this would result in an error as we did not create the struct with the `mut` keyword. Unlike languages like C#, the entire struct must be either mutable or immutable, you cannot delcare specific fields to be mutable.

```
let mut p = Point{ x: 3, y: 4 };
```

If you're familiar with **ES6 JavaScript** then you're probably aware of enhanced object literal syntax which allows you to declare just the property name if a variable exists in scope with the same name as the property. Rust has that too:

```
let x = 3;
let y = 4;
let p = Point{ x, y };
```

Similary, in JavaScript, you can spread an object into another one which you can also do in Rust:

```
let p = Point{ x, y };
let p2 = Point{ x: 10, ..p };
```

### Struct Methods

Methods are like functions except they are defined on structs. To define a method on a struct:

```
struct Square {
    length: u32,
}

impl Square {
    fn area(&self) -> u32 {
        self.length * 4
    }
}

...

let s = Square{length: 3};
s.area();
```

The `impl` keyword stands for `implementation` which creates an implementation block to define our method in. Rust implicitly passes a reference to the struct as the first argument to the method. Here we are borrowing `self`, but the method can also take ownership of it or borrow a mutable copy. Also, Rust has automatic referencing and deferencing so given the receiver of our method (&self in this case), Rust will automatically call the method with the proper receiver.

There are also `associated methods` which are similar to static methods in OOP languages. An associated method is defined the same way:

```
impl Square {
    fn from(length: u32) -> Rectangle {
        Square{ length }
    }
}
```

The key difference is that the method has no receiver and it is also invoked differently:

```
let s = Square::from(3);
```
