---
title: 'Intro to Rust - Ownership'
date: 2020-03-02
draft: false
tags: ['rust', 'intro']
---

Every programming language has to have some way to manage the memory it consumes while the program is running. In higher level languages like JavaScript this is managed with a garbage collector or with lower level languages like C, the memory is allocated and freed manually. Rust uses a different approach with a concept known as _ownership_.

### Stack and Heap

The stack and heap are parts of memory that your program can utilize at runtime. The stack stores values in memory in a LIFO (last-in-first-out) order. A common analogy is to think of a stack of plates. You can add plates on top of one another but you can't remove a plate from the middle, you have to remove the top most plate first. In programming parlance, adding a plate is called **pushing** onto the stack and removing the top plate is called **popping** off the stack. With stack memory, the size of each piece of data needs to be known in advance. If the size of the data is unknown then it is stored on the heap instead.

The heap is not as organized as the stack. Think of it like a restaurant and the operating system is acting as the hostess. You can request a table (memory) big enough for your party (data) and the hostess will search for an empty spot and have you seated there. When someone comes in late, the hostess can point them to that table. However, this is a slow process because the operating system has to continually search for areas large enough to store the data you want whereas with a stack, the new data is just pushed on top. Also, accessing data is slower to because the hostess (operating system) has to lead you to the table where the data was stored. In summary, a programmer usually has to think about where their data is being stored and clean up after themselves to achieve maximum performance, but we're human so this is source of a lot of bugs.

Take for example the `str` type in Rust:

```
let s = "Hello, World!";
```

This is a **string literal** because the size of the string is known at compile time. However, what if we don't know what the size of the string will be? Say if we ask the user to enter some sort of unknown sized input. In that case, there is a `String` type:

```
let s = String::new();
```

This supports a growable piece of text and is allocated on the heap, but Rust has to ask the operating system to do this at runtime and we also need a way to free the memory once we're done with it. Rust's concept of ownership seeks to address this issue for us.

### Ownership

To understand ownership, there are some ground rules that need to be outlined:

1. Every value in Rust has an owner.
2. There can only be one owner for a value.
3. When the owner of a value is out of scope, the value is dropped.

Using the example above, if we wrote:

```
{
    let s = String::new();
}
```

The scope starts at the first curly bracket and the value is allocated onto the heap. Once it reaches the closing bracket, the value is out of scope and is dropped for us by Rust without requiring that we manually free it ourselves.

This poses a problem though, what if we did something like this:

```
{
    let s = String::new();
    let z = s;
}
```

If you're familiar with how pointers work in other languages, the runtime does _not_ copy the entire value that `s` is pointing at to `z`. The reason for that is it would be extremely inefficient if the data was large. Instead, the pointer is copied to `z` so `s` and `z` now point to the same string in memory. The problem occurs when `s` and `z` both go out of scope and the runtime tries to free the value that both variables are pointing at **twice**. This is referred to as a **double free** error. The way Rust handles this is through ownership: when you re-assign `s` to `z` then `z` becomes the new owner of that value. The ownership has **moved**. Now if you tried to access `s` after its re-assignment, you would receive an error message. Once both variables go out of scope, Rust doesn't have to worry about deallocating `s` as it no longer considers it valid.

There are times we actually want to copy a value though so how would we do that without moving ownership? With Rust, we can **clone** the value instead:

```
{
    let s = String::new();
    let z = s.clone();
}
```

Now this actually does make an entire copy on the heap where `s` and `z` are both accessible. This issue of moving/cloning only affects values stored on the heap which is why the following code works fine:

```
{
    let a = 3;
    let b = a;
    // Can still access 'a'
}
```

These values are stored on the stack so copies are simple to make for Rust.

### Functions

So how do the rules of ownership apply when moving across a function boundary? The rules are essentially the same. You can move or copy values when calling a function and you can also return ownership after by returning the value to the caller. This raises an issue though: what if we want to pass a value into a function, but also not have it take ownership? Because if that were the case, we would have to return that value to retake ownership every time. Rust solves this via `referencing` and `borrowing`. A reference allows you to refer to a value without taking ownership of it. We denote a reference using an ampersand `&`:

```
let s = String::from("Hello, World!");

some_func(&s);

...

fn some_func(s: &String) {
    ...
}
```

Now when we pass `&s` into the function and the function returns, it will not try to free the memory point at by `s`. When a function has a parameter that is a reference type, it is called `borrowing`. There is a caveat with this though, when you try to change a value that is borrowed, you will encounter an error! If you want to mutate the value then you must ensure you declare the value as mutable:

```
some_func(&mut s);

fn some_func(s: &mut String) {
    ...
}
```

Now we can modify `s` inside of the function. Another important thing to note is that you can only have **one** mutable reference in a scope. For example, this is not allowed:

```
let mut x = &mut s;
let mut y = &mut s;
```

This is prohibited to prevent race conditions when multiple areas are trying to access the same variable simultaneously.
