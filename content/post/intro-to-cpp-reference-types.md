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

This is read as "ptr is a pointer to an integer".
