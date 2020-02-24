---
title: 'Intro to Typescript - Getting Started'
date: 2020-02-24T10:48:11-08:00
draft: false
---

### What is TypeScript?

TypeScript is a transpile-to-JavaScript language meaning that a program written in Typescript must first be translated (transpiled) to JavaScript before it can be run in the browser. Although compiling typically has a different meaning, the TypeScript community refers to this process as compilation. Why would anyone want to go through this process though? Because TypeScript comes with a host of features on top of those already available in JavaScript, all aimed at making writing JavaScript code more robust. The chief among those features is TypeScript's static type checking.

In a statically typed language, you declare variables of a certain type and any attempt to assign a value of a different type to that variable will result in a compilation error. In normal JavaScript, you can do stuff like:

```
let myStr = "Hello, World"
myStr = 26
```

Here we can assign a string to a variable and then re-assign it to be a number. However, in TypeScript, declaring a variable as a string and re-assgining it to a number results in an error:

```
let myStr: string = "Hello World"
myStr = 26

// Error
Type '26' is not assignable to type 'string'.(2322)
```

This type system alone eliminates a whole class of possible runtime errors by checking the types of variables at compile time. And the best thing about it is it's entirely optional. You don't _have_ to opt-in to the type system and you can still reap the benefits of having your program transpiled down to ES5 (something that previously required a transpiler like babel).

### Getting started

You'll need [Node](https://nodejs.org/en/) in order to install TypeScript. Once Node is installed you can run:

```
npm i -g typescript
```

You'll know it's installed properly if the following command logs the version:

```
tsc -v
```

Now create a `main.ts` file with the following content:

```
const add = (x: number, y: number) => {
    return x + y
}

console.log(add(3, 4))
```

You can then compile and run the program with:

```
tsc main.ts
node main.js
```

Try replacing one of the arguments with a value that is not a number:

```
console.log(add(3, "4"))
```

You'll see we get an error message along the lines of:

```
main.ts:5:20 - error TS2345: Argument of type '"4"' is not assignable to parameter of type 'number'.
```

**However**, the Typescript compiler still compiled the program us and we can run it because it's still a valid JavaScript program. We could tell TypeScript to not do that by adding a `--noEmitOnError` flag, but no one wants to type that every time you compile. To remedy that, we can create a config file called `tsconfig.json` and add our settings:

```
{
    "compilerOptions": {
        "noEmitOnError": true,
        "watch": true
    }
}
```

Note that we also added the `watch` property which will monitor `.ts` files for changes and recompile our code for us. To run the program now, we only have to type:

```
tsc
```

The TypeScript compiler can also generate the `tsconfig.json` file for you with sensible defaults by running:

```
tsc --init
```
