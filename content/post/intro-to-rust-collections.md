---
title: 'Intro to Rust Collections'
date: 2020-03-06
draft: false
---

Collections are data structures that contain multiple values. However, unlike arrays and tuples that are stored on the stack, these types are stored on the heap.

### Vectors

Vectors are similar to arrays except they can grow dynamically. Like an array, it can only store a single data type. To a create a new vector, we write:

```
let a: Vec<u32> = Vec::new();
```

The type annotation above is necessary as we've created an empty vector so Rust has nothing to infer from. Rust provides a macro to initialize a vector with some values:

```
let mut a = vec![1, 2, 3];
```

To add new values into the vector (make sure the variable is mutable):

```
a.push(4);
a.push(5);
```

To access an element at a specific index:

```
let el: &u32 = &a[2];

// or

match a.get(2) {
    Some(el) => println!("{}", el),
    None => println!("Nothing here");
}
```

The difference between the two is that the first method will panic if nothing exists at the index we are accessing.

It is also important to note that accessing an element with the first method borrows the variable so you cannot mutate the vector in the same scope:

```
let el: &u32 = &a[2];
a.push(8); // ERROR
```

The reason being is that a vector can grow dynamically and as a result, it might need to be allocated in another spot on the heap to do that.

To iterate over a vector:

```
let mut a = vec![1, 2, 3];

for n in &mut a {
    *n += 50;
}
```

We must provide a reference to the vector for the loop otherwise Rust will move the value and it will no longer be accessible outside. The asterisk dereferences `n` so we can access the value at that location and increment it.

I initially said that vectors can only hold a single type, but that isn't entirely accurate. You can store a vector of enums and each variant of that enum can hold a different type making it possible.

### Strings

The String type (not &str which is stored in the binary) is a growable and mutable UTF-8 string. To create a String:

```
let s = String::new();
```

To create a string literal (`&str`) we just use quotes:

```
let s = "abc";
```

You can transform a string literal into a String with the `.to_string()` or `String::from()` methods:

```
let a = s.to_string();
```

To append to a String, we can use `.push_str()`:

```
let mut a = String::from("abc");
a.push_str("def");
```

You can also concatenate strings using the `+` sign as with other languageS:

```
let a = String::from("abc");
let b = String::from("def");
let c = a + &b;
```

The important thing to note here is that `a` will no longer be accessible since it has been moved. Also note that `b` is a reference because you cannot add two `String` types together. If you wanted to add more than two strings together, it becomes a bit of a readability problem:

```
let a = String::from("abc");
let b = String::from("def");
let c = String::from("ghi");
let d = a + &b + &b;
```

So you can use the `format!` macro instead:

```
let d = format!("{}{}{}", a, b, c);
```

It's important to note that strings do not support indexing in Rust. A String is simply a wrapper around `Vec<u8>`, but that does not mean each single character takes only a single byte. Some characters in UTF-8 occupy multiple bytes so if you have a two-letter word and and the second character occupies two bytes, trying to access `word[2]` would be accessing the second byte of that second letter yielding something entirely different. Hold on though, why can we then slice a string? While you can do that, if you try to slice on a character boundary, Rust will panic at runtime.

Regardless, you can still iterate over a string:

```
for c in "word".chars() {
    println!("{}", c);
}
```

### Hash Maps

A hash map is like a dicitonary in Python or C# or an object literal in JavaScript; it maps a key of type `K` to a value of type `V` and are useful for quick lookups. To create a new hash map, we'll need to include it first:

```
use std::collections::HashMap;

let mut scores = HashMap::new();

scores.insert(String::from("abc"), 10);
```

All of the keys of a hash map must be of the same type as well as its values. You can also form a hash map from collecting two vectors:

```
let a = vec![1, 2, 3];
let b = vec![String::from("a"), String::from("b"), String::from("c")];

let c = HashMap<_, _> = a.iter().zip(b.iter()).collect();
```

Values that are owned will be moved into the hash map while types that implement the `Copy` trait will be copied. You can also insert a reference into the hash map as long as the references are valid for the time the hash map is.

To access a value in a hash map we can use `.get()`:

```
c.get(&b[0]);
```

Similarly to vectors, the .get() method can be a `Some` or `None` type in case we access a key that does not exist. To iterate over a hash map:

```
for (key, value) in &c {
    ...
}
```

To add a value, we can use `.insert()`:

```
c.insert(4, String::from("z"));
```

And if you want to check if the key already exists (so you don't overwrite the value):

```
c.entry(4).or_insert(String::from("z"));
```
