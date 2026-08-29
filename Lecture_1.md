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

- Shadowing: *Shadowing lets us reuse the guess variable name rather than forcing us to create two unique variables.* Read [Chap 3 Shadowing](https://rust-book.cs.brown.edu/ch03-01-variables-and-mutability.html#shadowing)

- trim: It deletes whitespaces and `\n`, and `\r\n`.

- parse: *The `parse` method will only work on characters that can logically be converted into numbers and so can easily cause errors.*

- loop: It creates an infinite loop.

- `_`: catch-all value. In `match [expression] {Err(_)}`, `Err(_)` will match all error types.

### Types in Rust

*Keep in mind that Rust is a statically typed language, which means that it must know the types of all variables at compile time.*

- [Rust book](https://rust-book.cs.brown.edu/ch03-02-data-types.html)
- [w3schools](https://www.w3schools.com/rust/rust_data_types.php)

;[Integer Overflow](https://rust-book.cs.brown.edu/ch03-02-data-types.html#integer-overflow)

Default type for integer is `i32`, default type of float is `f64`

Be careful about `char`, read [Chap 3](https://rust-book.cs.brown.edu/ch03-02-data-types.html#the-character-type)

### Compound types

#### Tuples

Elements in tuples can have different types.

- Tuples: `let t: (i32, f64, u8) = (500, 6.4, 1);` [Tuples and destructing](https://rust-book.cs.brown.edu/ch03-02-data-types.html#the-tuple-type)
- Tuple destructuring: `let (x, y, z) = t;`
- Tuple access: `t.0`, `t.1`
- Tuples without any values are called "unit". Like `let unit: () = ();`, see, its type is `()`, and itself is also `()`.

#### Arrays

Elements in an array must be the same type.

- Array: `let a: [i32; 5] = [1, 2, 3, 4, 5];`
- Array constructor: `let a: [i32; 5] = [3; 5];`. a is `[3,3,3,3,3]`
- Array access: `a[0]`

### Statements and expressions

The following statements are copied from [the Rust book](https://rust-book.cs.brown.edu/ch03-03-how-functions-work.html#statements-and-expressions)

- *Statements are instructions that perform some action and do not return a value.*
- *Expressions evaluate to a resultant value.* *Expressions do not include ending semicolons*
- *If you add a semicolon to the end of an expression, you turn it into a statement, and it will then not return a value.*

*You can return early from a function by using the return keyword and specifying a value, but most functions return the last expression implicitly.*

### Control flow

[The Rust book](https://rust-book.cs.brown.edu/ch03-05-control-flow.html)

#### If

Difference between Rust and C++

- The condition in Rust is not in braces '()', for example, `if x > 0 {}`.
- The condition must be bool. `let x = 3; if x {}` is invalid.

If your code has too many `else if`, consider refactor with `match`.

If one arm of `if {} else {}` returns (is a expression), then the other arm must return a value with **same type**. Because we may assign its value to variable (even if we don't assign, they still needs to be the same), `let x = if true {6} else {6};`. If two arms may return different types, then compiler don't know `x`'s type during compile time, this is forbidden in Rust.

Remember, **the type of all variables must be known during compile time.**

```rust
// This is valid, although x is immutable, 
// but Rust compiler knows it is assigned only once.
fn main() {
    let x;
    if true {
      x = 1;
    } else {
      x = 2;
    }
    println!("{x}");
}
```

#### loop, while, and for

`loop {}` is an infinite loop. Exit it either by `Ctrl+C` or `break;`. `while` is conditional loop.

`break` can also return values from a loop. e.g.

```rust
fn main() {
    let mut counter = 0;
    let result = loop {
        counter += 1;
        if counter == 10 {
            break counter * 2; // Or break counter * 2 (without ';')
        }
    };
    println!("The result is {result}"); // The result is 20
}
```

You can break specific loop, read [the Rust book, Disambiguating with Loop Labels](https://rust-book.cs.brown.edu/ch03-05-control-flow.html#disambiguating-with-loop-labels)

## My thoughts

Why the default type of Rust is immutable, you have to explicitly add a `mut` to make it mutable? -> I think it's because in C++, we should use `const` (similar to immutable) everywhere as long as possible. So, it is better to set the default type `const` in C++ (immutable in Rust). Notice there is [difference between constant and immutable](https://rust-book.cs.brown.edu/ch03-01-variables-and-mutability.html#declaring-constants). The Rust constants are more like C++ micros.
