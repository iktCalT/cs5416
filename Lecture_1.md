# Lecture 1

C++ -> Rust
75% Project -> 18% Project

## Overview of Rust

- Rust programming
- Writing fast code
- Unix abstractions
- Concurrent programming
- Async programming

Write a platform for multiplayer.

## Prerequisite

Program in C
Know Unix kernel is dangerous
Know computer org

## Logistic

- Reding: CSAPP
- Class sheets 10
- Lab/discussion, bring laptop 12
- Projects 18
- Midterm 20, Rust
- Final 40, concepts

## Intro to Rust

Reference: [The Rust Programming Language](https://doc.rust-lang.org/book/) and [The Rust Programming Language (Brown version)](https://rust-book.cs.brown.edu/)

`rustup` is used to *manage Rust versions and associated tools*. Rust files always end up with `.rs`, `rustc` is rust compiler (for example, run `rustc ./hello.rc` will output a binary file `hello`, then you can run it with `./hello`)

`println!` is a rust macro (macros end up with `!`).

*Cargo is Rust’s build system and package manager.*. Use `cargo new project_name` to create a project. If it's not in a git repository, it will initialize a git repo for you. To turn rust files into a rust project, read [Chap 1-3](https://rust-book.cs.brown.edu/ch01-03-hello-cargo.html#creating-a-project-with-cargo).

To build a cargo project, use `cargo build` in your project directory. The default mode is **debug** mode. So, it will create a binary file in debug directory (`target/debug/hello`). It will also create a `Cargo.lock` file, which *keeps track of the exact versions of dependencies in your project*.

To build in ***release*** mode, use `cargo build --release` (but it takes longer to compile). It will generate a executable file in `target/release`.

You can use `cargo run` to compile & run. This command is more convenient, and most developers use `cargo run`. If the file (newest version) has already been compiled, it will just run it.

You can use `cargo check` to check if your project is compiled or not (and this command won't start compiling, so it saves time). But if you modified source file, it won't detect it. It is useful because it *lets you know if your project is still compiling*

[`cargo update`](https://rust-book.cs.brown.edu/ch02-00-guessing-game-tutorial.html?#updating-a-crate-to-get-a-new-version) will update a crate (collection of Rust **source code** files).

> [!Note]
> Cargo does not watch your files by default. But you can use plugins like cargo-watch for this purpose. Read [the quiz part of *Hello, Cargo!*](https://rust-book.cs.brown.edu/ch01-03-hello-cargo.html#leveraging-cargos-conventions). But it will read the metadata (timestamp etc.) to see if file is modified (potentially). If it could be modified, it will call `rustc`. Then `rustc` will recompile for you. If it's a minor change, recompilation won't take long (due to local cache).

Use `cargo doc --open` to generate a document of all dependencies used in your project. Very useful.

## Syntaxes of Rust

[Chap 2](https://rust-book.cs.brown.edu/ch02-00-guessing-game-tutorial.html) of the Rust book gives examples. [Chap 3](https://rust-book.cs.brown.edu/ch03-00-common-programming-concepts.html) explains them in detail.

- `let a = 1;` creates a immutable variable, Rust can deduce its type is int([`i32` by default](https://rust-book.cs.brown.edu/ch02-00-guessing-game-tutorial.html?#comparing-the-guess-to-the-secret-number)).
- You can assign a mutable variable with `let mut a = 1;`.
- You can explicitly assign a type like `let mut a: i8 = 1`. (`i8` means 8-bit integer) for [more types](#types-in-rust):
- Notice that chars in Rust are UTF-8 encoded (meaning it is NOT fixed-sized). So, you cannot use index to navigate chars in a string directly.

> *By default, Rust has a set of items defined in the standard library that it brings into the scope of every program. This set is called the **prelude**. If a type you want to use isn’t in the prelude, you have to bring that type into scope explicitly with a `use` statement* (just like `#include` in C++, and `import` in Python).

- `match` expression
  Read [Chap 2 Comparing the Guess to the Secret Number](https://rust-book.cs.brown.edu/ch02-00-guessing-game-tutorial.html?#comparing-the-guess-to-the-secret-number)

  After match find first matching arm, it won't look at following arms.

- Shadowing: *Shadowing lets us reuse the guess variable name rather than forcing us to create two unique variables.*

- trim: It deletes whitespaces and `\n`, and `\r\n`.

- parse: *The `parse` method will only work on characters that can logically be converted into numbers and so can easily cause errors.*

- loop: It creates an infinite loop.

- `_`: catch-all value. In `match [expression] {Err(_)}`, `Err(_)` will match all error types.

### Types in Rust

- [Rust book](https://rust-book.cs.brown.edu/ch03-02-data-types.html)
- [w3schools](https://www.w3schools.com/rust/rust_data_types.php)

## My thoughts

Why the default type of Rust is immutable, you have to explicitly add a `mut` to make it mutable? -> I think it's because in C++, we should use `const` (similar to immutable) everywhere as long as possible. So, it is better to set the default type `const` (immutable).
