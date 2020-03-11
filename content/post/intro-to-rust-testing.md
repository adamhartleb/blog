---
title: 'Intro to Rust - Testing'
date: 2020-03-10T19:11:26-07:00
draft: true
tags: ['rust', 'intro']
---

While Rust was designed with correctness as a first class concern, proving correctness is extremely complex and not an easy task. As a result, Rust includes automated tests as part of the language. Rust will check that all your types and references to ensure they're valid, but it can't check your logic. If you create a function that is supposed to remove the suffix of a word, but it doesn't _actually_ do that, that is where tests come in.

A test in Rust is just a function that is annotated with the `test` attribute. Here's an example:

```
#[cfg(test)]
mod tests {
    #[test]
    fn it_works() {
        assert_eq!(2 + 2, 4);
    }
}
```

The `#[test]` part is the attribute that indicates this a test function. The reason that is required is because we can also have non-test functions in our suite to help set up the tests. Within the test we use the `assert_eq!` macro which asserts that the received value matches the expected value. To run the tests:

```
cargo test
```

And we will see that the test has succeded. One of the ways to get a test to fail is to panic:

```
#[test]
fn it_fails() {
  panic!("This will fail");
}
```

The two common ways to test equality are to use the `assert_eq!` and `assert_ne!` macros. Under the surface these two macros simply use `==` and `!=` to compare the values. Both types you're comparing must implement the `PartialEq` and `Debug` traits. All primitive types implement these traits, but for types like structs and enums, you'll need to implement those yourself.

We can add custom error messages when the tests fail by passing a second argument to the `assert!` macro:

```
let result = add_one(2);
assert!(result, "Expected 3, but received {}", result);
```

In order for us to check if our code panics, we can add another attribute called `#[should_panic]` to our test. If the test panics, then it will pass if the attribute is present.

```
#[test]
#[should_panic]
fn this_will_pass() {
  panic!("Oh no!");
}
```

Consequently, if the test does not panic, then it will fail.
