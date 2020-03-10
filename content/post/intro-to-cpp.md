---
title: 'Intro to C++ - Getting Started'
date: 2020-03-10
draft: false
tags: ['cpp', 'intro']
---

To begin, we write human-redable C++ code in a _source file_ which is then _compiled_ to produce machine code that our computers can run. Here's an example of a minimal source file:

```
// main.cpp
#include <cstdio>

int main() {
    printf("Hello, World!");
    return 0;
}
```

The above declares a function called `main` which serves as an entry point to our program, after all, the program has to stat somewhere. Within our `main` function we call another function `printf` which prints the text to the terminal. Finally, we return `0` from our function which is known as an **exit code**. Exit codes are integer values that tell the operating system what happened after the program ran. An exit code of `0` means the program ran successfully.

You probably noticed the `#include <cstdio>` part as well. That is necessary to include because the `printf` is not defined in our program so we have to include its definition in. This is similar to other languages like JavaScript where we import modules via `require`.

### Compiler

Once we've written our source code, it's time to compile it to machine code. The compiler has three steps:

1. The preprocessor manipulates our source code by bringing in the code we included from other files (like our include directive). The result of this stage is a **translation unit**. A translation unit is the basic unit of compilation in C++. It consists of the contents of a single source file, plus the contents of any header files directly or indirectly included by it.

2. The compiler then takes that translation unit and turns it into an **object file** which is the machine code our computer will execute, but not yet. The reason for this intermediary step is it allows us to make incremental builds. You can compile each source file separately without having to recompile the entire program.

3. The final stage is the linker. This is what generates an executable program from our object files. The linker is also responsible for re-arranging your code and filling in the missing parts so that functions in some pieces can successfully call functions defined in other ones.

To get started compiling our source code we can install a compiler. On Windows, we'll use [MinGW](http://www.mingw.org/). Once that is install and compiled, we can write the following in our terminal:

```
gcc main.cpp -o main
main
```

Which will then print "Hello, World!" to our terminal.

### Basics

Variables in C++ are declared by stating their type first followed by the name of the variable:

```
int x;
```

We can also initialize the variable with a value on the same line:

```
int x = 3;
```

A conditional statement allows us to control the flow of our program. Some basic conditionals include the `if` statement:

```
if (boolean-expression) {
    // do stuff
} else if (another-boolean-expression) {
    // other stuff
} else {
    // ...
}
```

Functions are blocks of code that accept inputs (arguments) and return an output. A function has the following structure:

```
return_type function_name(paramter_1, parameter_2) {
    return return_value;
}
```

An actual implementation looks like:

```
bool isEven(int x) {
    if (x % 2 == 0) {
        return true;
    }

    return false;
}
```

And to call the function we write:

```
bool result = isEven(4);
```

Comments are notes developers leave for future reference. A single line comment beings with two forward slashes (`//`):

```
// This is a comment
```

And multi-line comment begins with `/*` and ends with `*/`:

```
/* this is a multi
line comment */
```
