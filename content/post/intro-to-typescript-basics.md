---
title: 'Intro to Typescript - Basics'
date: 2020-02-25T15:18:09-08:00
draft: true
tags: ['typescript', 'intro']
---

### Declaring variables with Types

To declare a variable with a type in TypeScript, we add a colon after the name of the variable:

```
let x: number = 3;
let y: string = "Adam";
```

The following types can be assigned: `number`, `boolean`, `string`, `any`, `null` `unknown`, `symbol`, `void`, `never`. Most of these you will recognize if you've programmed in JavaScript or any other language, but there are couple that might be new. The `any` type means the type can be anything which is essentially the default in regular JavaScript. The `void` type is just an alias for `undefined` meaning the absence of a type and is used to indicate the return value in a function header. The `unknown` type is similar to `any` in that any type can be assigned to it, but with `any` you can perform operations on it whereas with `unknown` you must first assert/narrow the type before operating on it. Finally, `never` is an interesting one because it means that the code is unreachable. This is reserved for things such as infinite loops in a function because that function cannot return anything.

In general, you should avoid type annotations if the TypeScript compiler can infer the type from the assignment during initialization. If you're declaring a type to be assigned later, then add the type annotation. Type annotations should always be added to function headers.

### Function declarations with Types

For function definitions, we can declare the types of each parameter as well as the return type after the parameter list. For example:

```
const calcTip = (total: number, tipPercent: number): number => {
    return total * tipPercent
}
```
