---
title: 'Intro to Rust - Hello World'
date: 2020-02-24T15:06:48-08:00
draft: true
---

Installing and configuring Rust is a breeze with **rustup** which is an installer for Rust. You can download it by visiting:

https://rustup.rs/

And following the onscreen instructions. You can confirm that the installation has worked by running:

```
rustc --version
```

The rustup installation also comes with another command line tool called **cargo** which is the Rust packager manager -- akin to **npm** for Node. Rust packages are called **crates** and there is an online repository of crates visible here:

https://crates.io/

To start a new Rust project, we'll run the following command:

```
cargo new --bin helloworld
```

This will create a new folder called `helloworld` in your current working directory. The `--bin` flag creates a new binary crate which compiles into an executable to run. The alternative is a library crate `--lib` that are meant to be used in other projects.

Inside the `helloworld` directory, you'll find a file called `Cargo.toml` which contains metadata and dependencies in our application (similar to `package.json` from npm) as well as the `src` directory where our source code lives. Inside the `src` folder you'll find a `main.rs` file with your typical "Hello, world" program ready to run. To run the program we can run:

```
cargo build
```

This command generates some new files for us. It first creates a `Cargo.lock` which keeps track of the exact versions of the dependencies we used if we had any and a `target` folder. In `target` there's another folder called `debug` that contains the executable. We can now run our program:

```
<!-- Use forward slashes on UNIX systems. -->

.\target\debug\helloworld
```

The command above creates an unoptimized debug version of our code. If we want to prepare it for production, we can add the `--release` flag. Since we'll be frequently building and running our code in development, cargo provide a two-in-one command via:

```
cargo run
```

Most importantly, your rustup installation comes with all the documentation for Rust as well as **an entire book on learning Rust** locally on your computer. You can access the documentation, by running:

```
rustup doc
```
