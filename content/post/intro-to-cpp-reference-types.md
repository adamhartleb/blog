---
title: 'Intro to C++ - Reference Types'
date: 2020-03-14T11:38:58-07:00
draft: true
tags: ['cpp', 'intro']
---

Reference types store the memory address (pointer) to values rather than storing the memory address of the values directly.

### Pointers

Pointers are the fundamental mechanism used to interact with memory addresses. A pointer holds the address of the object as well as its type. To declare a pointer, we use an asterisk:

```
int* ptr;
```

This is read as "ptr is a pointer to an integer". That is to say that `ptr` simply holds the memory address (not the value at the memory addess) of where the integer is located. In order to assign a memory address to a pointer variable, we use the address-of operator which is the ampersand symbol:
```
int x = 3;
int* y = &x;
```
Here we are storing the memory address of the variable `x` into the variable `y`. To print out the value of a pointer we can use the `%p` format specifier. A fun fact: you won't get the same memory address printed out each time and that's due to a concept called **address space layout randomization**. It aids in defending against hackers who try to inject a malicious payload and get your program to execute it by randomizing the memory addresses our program uses. This way, they won't know where to inject the payload into memory.

Now that we have the address, how do we access the value at that address? We can use the dereferencing operator which is an asterisk:
```
int x = 3;
int* y = &x;
int z = *y;
```
Here we are dereferencing the pointer `y` to get the value it is pointing at (the value stored in `x`).