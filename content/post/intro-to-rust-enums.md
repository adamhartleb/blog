---
title: 'Intro to Rust - Enums'
date: 2020-03-05
draft: true
tags: ['rust', 'intro']
---

An enumerations or more commonly know as _enum_ allows you to define a type with a set number of possible values. To declare an enum, we write:

```
enum Seasons {
    Spring,
    Summer,
    Fall,
    Winter,
}
```

Each option in an enum is referred to as a `variant`. To assign an enum value to a variable:

```
let currentSeason = Season::Spring;
```

You can also associate a certian data type with each variant. For example, if you wanted each season to be represented by a number:

```
enum Seasons {
    Spring(u8),
    Summer(u8),
    Fall(u8),
    Winter(u8),
}


let currentSeason = Season::Spring(0);

```

Similar to structs, you can also define methods on enums:

```
impl Seaons {
    fn something(&self) {
        ...
    }
}

let s = Seasons::Spring(0);
s.something();
```

### Option Enum

One of the enums defined in the standard library is the `Option` enum type which represents the case where a value could be something or it could be nothing.

```
enum Option<T> {
    Some(T),
    None,
}
```

The use of this enum allows Rust to check if all possible values have been handled at compile time. If you don't handle the None case, then the program won't compile.

### Extracting Values

As shown earlier, we can associate a data type with an enum, but how can we extract that value? We can achieve that through pattern matching:

```
let s = Season::Winter(3);
match {
    Seasons::Winter(val) => {
        println!("We extracted {}", val);
    },
    // Add matching cases for other seasons
}
```
