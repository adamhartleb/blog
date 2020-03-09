---
title: 'Intro to Rust - Generics'
date: 2020-03-09
draft: true
tags: ['rust', 'intro']
---

Generics allow us to reduce code duplication which leads to less errors as well as better maintainability in our code base. A simple example of a function that can be generalized is one that finds the largest value in a list of elements:

```
fn find_largest_num(list: &Vec<i32>) -> i32 {
    let mut largest_num = list[0];

    for &n in list {
        if n > largest_num {
            largest_num = n;
        }
    }

    return largest_num;
}
```

The issue with this function is that it only accepts a list of `i32`. If we had a list of `i64` or `u32`, we would have to create separate functions for those. With generics, we can re-write the function as:

```
fn find_largest_num<T>(list: &Vec<T>) -> T {
    let mut largest_num = list[0];

    for &n in list {
        if n > largest_num {
            largest_num = n;
        }
    }

    return largest_num;
}
```

Generics are not limited to functions though, we can use them in structs as well:

```
struct Point<T> {
    x: T,
    y: T,
}
```

Note that when creating this struct, you're restricted to a single type and all fields must be of that type. If you wanted to have multiple possible types, you can write:

```
struct Point<T,U> {
    x: T,
    y: U,
}
```

Generics can also be used with enums:

```
enum Result<T, E> {
    Some(T),
    Err(E),
}
```

And with method definitions:

```
impl<T> Point<T> {
    fn x(&self) -> &T {
        &self.x
    }
}
```

If you only want to define the method on a certain instance of a type, you can do that as well:

```
impl<i32> Point<i32> {
    fn x(&self) -> i32 {
        self.x
    }
}
```

The best part about generics is that there is no runtime cost for them. Rust uses a process called _monomorphization_ which fills in the concrete types for the generics at compile time.

### Traits

There is another problem with the generic verison of `find_largest_num` we defined earlier: it only works with types that can be compared, but since it's generic, it can accept any type. How can we constrain it to work with a generic number type only?

That's where traits come in. Traits are similar to interfaces in languages like C#. A trait tells the Rust compiler about the functionality a specific type has. We can create a trait like so:

```
pub trait Summary {
   fn summarize(&self) -> String;
}

struct Tweet {
    name: String,
    body: String,
}
```

And to implement it:

```
impl Summary for Tweet {
    fn summarize(&self) -> String {
        return self.body;
    }
}

fn main() {
    let s = Tweet{name: "Adam", body: "Helloo"};
    println!("{}", s.summarize());
}
```

We can also accept traits as parameters. Back to our `find_largest_num` function, we can fix it by specifying that the argument passed in must implement two traits (`PartialOrd` and `Copy`):

```
fn largest<T: PartialOrd + Copy>(list: &[T]) -> T {
    let mut largest = list[0];

    for &item in list.iter() {
        if item > largest {
            largest = item;
        }
    }

    largest
}
```

The `+` symbol between the traits implies that both traits need to be implemented for the type.
