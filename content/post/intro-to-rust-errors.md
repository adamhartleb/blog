---
title: 'Intro to Rust - Errors'
date: 2020-03-07
draft: true
tags: ['rust', 'intro']
---

Rust has two major categories for errors: recoverable and unrecoverable. A recoverable error is like trying to read from a file that doesn't exist while an unrecoverable error comes from something like attempting to read an out-of-bounds index on an array.

You can throw your own unrecoverable errors as well with the `panic!` macro. In response to a panic, Rust will begin unwinding the call stack, cleaning up data along the way. This is a costly process so as an alternative, you can `abort` and the program immediately stops the program altogether.

Since most errors aren't that serious, we can respond to them with the `Result` enum.

```
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

As an example, we'll call a function that returns a `Result` type:

```
use std::fs::File;

fn main() {
    let f = File::open("hello.txt");
}
```

We can then take an action depending on the value that is returned:

```
let f = match f {
    Ok(file) => file,
    Err(e) => panic!(e),
};
```

Now this will handle all errors produce by `File::open` equally, but what if we wanted to handle specific errors differently? Here's how we would do that:

```
use std::io::ErrorKind;

let f = match f {
    Ok(file) => file,
    Err(e) => match error.kind() {
        ErrorKind::NotFound => match File::Create("hello.txt") {
            Ok(fc) => fc,
            Err(e) => panic!("Problem creating file: {:?}", e),
        },
        other_error => panic!("Problem opening the file: {:?}", e),
    },
};
```

Using and nesting match statements leads to verbose code though. The `Result` enum defines some methods on it like `unwrap` which is a shortcut for unwrapping the `Ok` value:

```
let f = File::open("hello.txt").unwrap();
```

However, this ignore the potential error which will cause a panic. Instead, we can write:

```
let f = File::open("hello.txt").expect("Something bad happened");
```

This will still cause the code to panic, but we can customize the error message to aid in debugging.

### Propogating Errors
