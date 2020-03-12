---
title: 'Intro to C++ - Types'
date: 2020-03-12T14:25:30-07:00
draft: true
tags: ['cpp', 'intro']
---

We'll be investigating the primitive types C++ has to offer in this post and reference types in the following post.

### Integers

The Integer type store whole numbers and come in four sizes: `short int`, `int`, `long int`, `long long int`. In addition, each type can be `signed` (negative whole numbers permitted) or `unsigned` (only positive numbers).

A `short` is typically 2 bytes in size and an `int` is 4 bytes. A `long` is 4 bytes on everything except on 64-bit Linxu/macOS where it is 8 bytes. A `long long` is 8 bytes.

You can specify the represenation of the integer as well since binary, octal and hexadeciaml represenations are supported. A binary number is prefixed with `0b`, an octal number with just `0` and a hexadecimal number with `0x`. Here are some examples:

```
#include <cstdio>

int main() {
    unsigned short int myInt = 0b101010;
    int a = 0123;
    signed long long anotherInt = 0xFFF;
}
```

### Floats

Floats store an approximation of a real number (due to the finiteness of memory). The amount of memory a float occupies is referred to as its `precision`. The higher the precision, the more accurate it will be at approximating the provided number. A `float` provides single precision (4 bytes) and a `double` provides double precision (8 bytes). Float literals are double precision by default. If you want to create a single precision literal, the number is suffixed with `f`:

```
float n = 3.14f;
```

### Characters

There are six character types: `char` which is the default type and stores one byte and is usually used for ASCII characters. `char16_t` is used for 2-byte characters sets like UTF-16. `char32_t` is for 4-byte sets like UTF-32. Additionally, the `char` type can be signed or unsigned. Finally, there is `wchar_t` which will be large enough to contain the implementation's locale.

A character literal is a single character enclosed with single quotes:

```
char letter = 'a';
```

If the character is anything but a char, it must be prefixed with `L` for `wchar_t` or `u` for `char16_t` and `U` for `char32_t`.

### Booleans

A boolean is a type with two states: `true` or `false`:

```
bool b = true;
```

### Misc

If working with raw memory without a specific type, there is the `std::byte` type defined in the `<cstddef>` header which is just a collection of bits.

Another type in the `<cstddef>` header is the `size_t` type which encodes the size of objects and is guaranteed to represent the maximum size of all objects. The `sizeof()` function returns a `size_t`.

The `void` type is only used for function to indicate it returns nothing.

### Arrays

An array is a sequence of identical types with a specified length. To create an array of 10 integers, we can write:

```
int myArray[10];
```

Or you can initialize it and allow the compiler to infer its length:

```
int myArray[] = {1, 2, 3};
```

To access an element in an array we use its 0-based index:

```
myArray[1];
```

### Loops

The standard for loop looks like:

```
for (int i = 0; i < 10; i++) {
    ...
}
```

The counter is intialized first, the condition is checked and then the body of the loop is executed. Afterward, the counter is incremented, the condition checked and so on.

There is also a range based for loop:

```
for (int i : myArray) {
    ...
}
```

Which provides a more declarative way of programming and reduces potential bugs like off-by-one errors.

To grab the number of the elements in an array, you can call `sizeof()` on the array and divide it by the result of calling `sizeof()` on the type of that array:

```
size_t numOfElements = sizeof(myArray) / sizeof(int);
```

### Strings

Like an array a string is a contiguous sequence of characters. A C-style string is such a contiguous block that ends with the null terminating character:

```
char sentence[] = "Hello there!";
```

### Enumerations

An enumeration is a fixed set of possible values. To declare an enumeration we write:

```
enum class Race {
    Orc,
    Troll,
    Tauren,
    Undead
};
```

And to assign it to a variable we write:

```
Race r = Race::Troll;
```

### Struct

Structs are user-defined types that can be conceptually thought of as an array of different types. To create a struct:

```
struct Person {
    int age;
    char[256] name;
};

int main() {
    Person p;
    p.age = 23;
}
```
