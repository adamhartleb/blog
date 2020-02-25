---
title: 'Intro to Rust - Variables'
date: 2020-02-26T10:48:11-08:00
draft: true
tags: ['rust', 'intro']
---

Variables are conceptually labeled boxes that we can store values. The box is the address in memory where the value is stored and the label is just a human readable alias for that address.

All variable declarations in Rust start with the `let` keyword followed by the name we assign to variable. Here we are declaring a variable called `z` and assigning the value `12` to it:

```
let z = 12;
```

By default, all variables in Rust are **immutable** meaning you cannot re-assign a value to them. For example, this will result in a `compiler error`:

```
fn main() {
    let z = 12;
    println!("Value of z is {}", z);
    z = 3;
    println!("Value of z is {}", z);
}
```

The reason Rust variables are immutable by default is because it removes a whole host of potential bugs. If you assume a value never changes, but another part of the program might change it, then it violates the mental model you had regarding that thread of execution. Programmers are human and cannot possibly conceptualize what every part of a non-trivial program is doing at a particular point in time so making variables immutable is a simple compromise.

However, if you do want a variable to change over time, you can opt into it using the `mut` keyword. Now we can see our program compiles successfully:

```
fn main() {
    let mut z = 12;
    println!("Value of z is {}", z);
    z = 3;
    println!("Value of z is {}", z);
}
```

All variables in Rust have types. In the code examples above, the compiler inferred the type of the variable from the value, but we can explicitly provide the type using a `colon (:)` follow by the type placed after the name of the variable:

```
let z: i32 = 12;
```

You can also assign multiple variables in a single statement. To do so, you wrap the names and values (and types if provided) in `parentheses ( )`:

```
let (x, y): (i32, i32) = (12, 13);
```

### Scope

The scope of a variable refers to the region in your code that other parts of your program can access its value. In terms of scope, there are two types of variables: `local` and `global`.

A local variable is scoped to the nearest `code block` which is delimited by curly braces `{ }`. After the closing curly brace, the variable is dropped from memory. Variables declared in outer code blocks can be accessed in inner code blocks, but the reverse is not true. You cannot access a variable in an inner scope from an outer scope. For example:

```
fn main() {
    let z = 12;

    {
        let y = 3;
        println!("I can access z {}", z);
    }

    println!("I cannot access y {}", y);
}
```

In order to create a global variable in Rust, you must use the `static` keyword and you must provide the type when declaring them. Their names also have to be capitalized or else you'll receive a compiler warning:

```
static N: i32 = 23;

fn main() {
    println!("{}", N);
}
```

Finally, you can declare a value with the `const` keyword instead of `let`. Variables declared with `const` live for the entire lifetime of a program and are not dropped. It follows similar rules with regards to `static` in that the name should be uppercased and the type has to be provided:

```
const N: i32 = 23;

fn main() {
    println!("{}", N);
}
```
