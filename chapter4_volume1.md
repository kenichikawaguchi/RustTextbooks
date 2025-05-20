# Chapter 4: Functions & Modules

**Goals:**  
- Understand how to define and call functions in Rust  
- Learn about scopes and return values  
- Organize code using modules and the `use` keyword  
- Distinguish between binary and library crates  

---

## 4.1 Defining Functions

Functions in Rust are declared using the `fn` keyword:

```rust
fn main() {
    println!("5 + 3 = {}", add(5, 3));
}

fn add(x: i32, y: i32) -> i32 {
    x + y  // no semicolon: expression returns value
}
```

- Parameters are type-annotated.  
- The return type follows `->`.  
- If a function body ends with an expression (no semicolon), that value is returned.

---

## 4.2 Scopes and Shadowing in Functions

Variables inside functions are scoped to that function:

```rust
fn main() {
    let x = 10;
    println!("x in main = {}", x);
    print_value(x);
    // println!("y in main = {}", y); // error: y not in scope
}

fn print_value(y: i32) {
    println!("y in print_value = {}", y);
}
```

- Each function has its own scope.  
- Shadowing applies within function bodies as usual.

---

## 4.3 Modules and the Filesystem

Rust modules organize code in a file hierarchy:

```
src/
├── main.rs
└── math/
    ├── mod.rs
    └── calculator.rs
```

- `mod math;` in `main.rs` loads `src/math/mod.rs`.  
- Inside `mod.rs`: `pub mod calculator;` to load `calculator.rs`.  
- Paths: `math::calculator::multiply(2, 3)`.

---

## 4.4 The `use` Keyword and Paths

Import names to shorten paths:

```rust
// src/main.rs
mod math;

use math::calculator::divide;

fn main() {
    println!("6 / 2 = {}", divide(6, 2));
}
```

- `use` brings items into scope.  
- You can alias: `use math::calculator as calc;`.

---

## 4.5 Binary vs. Library Crates

- **Binary crates** have a `main` function; produce executable.  
- **Library crates** expose functionality; include `lib.rs`.

Example `Cargo.toml` for mixed crate:

```toml
[package]
name = "simple_calculator"
version = "0.1.0"
edition = "2021"

[[bin]]
name = "calc"
path = "src/main.rs"
```

`src/lib.rs`:

```rust
pub mod math {
    pub mod calculator {
        pub fn add(a: i32, b: i32) -> i32 { a + b }
        pub fn subtract(a: i32, b: i32) -> i32 { a - b }
        pub fn multiply(a: i32, b: i32) -> i32 { a * b }
        pub fn divide(a: i32, b: i32) -> i32 { a / b }
    }
}
```

`src/main.rs`:

```rust
use simple_calculator::math::calculator::*;

fn main() {
    println!("2 + 3 = {}", add(2, 3));
    println!("5 - 1 = {}", subtract(5, 1));
    println!("4 * 7 = {}", multiply(4, 7));
    println!("8 / 2 = {}", divide(8, 2));
}
```

---

## Exercises

1. Write a function `greet(name: &str)` that prints "Hello, {name}!" and call it from `main`.  
2. Create a module `strings` with a function `capitalize(s: &str) -> String`. Practice `pub` and non-`pub`.  
3. Split the calculator example into modules as shown, then add an `exponent` function.  
4. Turn the calculator into a library crate only; write tests in `tests/` directory.  
5. Experiment with aliases: import functions under different names using `as`.  
