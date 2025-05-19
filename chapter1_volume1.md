# Chapter 1: Why Rust?

**Goals:**  
- Understand the motivations behind Rust  
- Appreciate Rust’s guarantees around safety and performance  
- Learn how to install the Rust toolchain  
- Get familiar with `rustc` vs. `cargo` workflows  

---

## 1.1 Motivation: What Makes Rust Special?

Rust was created to solve two long‑standing problems in systems programming:

1. **Memory Safety without a Garbage Collector**  
   - Rust’s *ownership* and *borrow checker* enforce at compile time that you never:
     - Use freed memory (use‑after‑free)  
     - Have data races in concurrent code  
   - Unlike C/C++, Rust gives you fine‑grained control over allocation and deallocation *without* a runtime GC pause.

2. **Zero‑Cost Abstractions**  
   - High‑level features (iterators, closures, async/await) compile down to the same machine code you’d write by hand in C.  
   - You pay only for what you use; if you don’t use a feature, you don’t pay for it in size or speed.

3. **Modern Tooling & Community**  
   - Built‑in package manager (Cargo), formatter (rustfmt), and linter (Clippy)  
   - Rapidly evolving ecosystem with first‑class support for WebAssembly, embedded, CLI, web backends, and more.

---

## 1.2 Installing the Rust Toolchain

Rustup is the recommended installer and version manager for Rust.

1. **On Linux and macOS**  
   ```bash
   curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
   ```

2. **On Windows**  
   ```powershell
   # Download and run the Rustup installer
   iex ((New-Object System.Net.WebClient).DownloadString('https://sh.rustup.rs'))
   ```

After installation, ensure your environment is set up:

```bash
rustup update          # Get the latest stable toolchain
rustup show            # See which toolchains are installed
rustc --version        # Verify the compiler is on PATH
cargo --version        # Verify Cargo is on PATH
```

---

## 1.3 `rustc` vs. `cargo`

### 1.3.1 `rustc` (Rust Compiler)

- Directly invokes the compiler on one `.rs` file.  
- Good for small experiments or teaching the basics.

Example:

```bash
# Compile a standalone file `hello.rs`
# hello.rs:
#   fn main() {
#       println!("Hello, world!");
#   }
rustc hello.rs
./hello   # run the binary
```

### 1.3.2 `cargo` (Rust’s Build System & Package Manager)

- Creates and manages *projects* (called “crates”).  
- Handles dependencies, builds, tests, benchmarks, and publishing.  
- Encourages a standardized project layout (`src/`, `Cargo.toml`, etc.).

Common commands:

| Command               | Description                                      |
|-----------------------|--------------------------------------------------|
| `cargo new my_app`    | Create a new binary crate in `my_app/`           |
| `cargo new --lib lib` | Create a new library crate in `lib/`             |
| `cargo build`         | Compile the current project                      |
| `cargo run`           | Build *and* run the `main()` function            |
| `cargo test`          | Run all tests in the crate                       |
| `cargo fmt`           | Auto‑format code according to Rust style         |
| `cargo clippy`        | Run the Clippy linter for additional warnings    |

Example workflow:

```bash
# 1. Create a new project
cargo new hello_rust
cd hello_rust

# 2. Build and run
cargo run
# → “Hello, world!”

# 3. Edit src/main.rs:
#    fn main() {
#        println!("The sum of 2 + 3 is {}!", 2 + 3);
#    }

# 4. Re‑run
cargo run
# → “The sum of 2 + 3 is 5!”
```

---

## 1.4 Your First Mini‑Project: “Guess the Number”

Let’s write a simple command‑line guessing game to try out:

```rust
// src/main.rs

use std::io;
use rand::Rng;           // External crate for random numbers
use std::cmp::Ordering;

fn main() {
    println!("Guess the number!");

    let secret = rand::thread_rng().gen_range(1..=100);

    loop {
        println!("Please input your guess.");

        let mut guess = String::new();
        io::stdin()
            .read_line(&mut guess)
            .expect("Failed to read line");

        let guess: u32 = match guess.trim().parse() {
            Ok(num) => num,
            Err(_)  => {
                println!("Please type a valid number!");
                continue;
            }
        };

        println!("You guessed: {}", guess);

        match guess.cmp(&secret) {
            Ordering::Less    => println!("Too small!"),
            Ordering::Greater => println!("Too big!"),
            Ordering::Equal   => {
                println!("You win!");
                break;
            }
        }
    }
}
```

1. **Add `rand` to your `Cargo.toml`:**

   ```toml
   [dependencies]
   rand = "0.8"
   ```

2. **Build and run:**

   ```bash
   cargo run
   ```

3. **Play!** Try guessing numbers between 1 and 100.

---

## 1.5 Summary & Exercises

- **Summary:**  
  - Rust combines performance, safety, and modern tooling.  
  - You learned to install Rust, and use `rustc` for small scripts vs. `cargo` for full projects.  
  - You built and ran your first “Hello, world!” and a mini guessing‑game.

- **Exercises:**  
  1. Modify the guessing game to give the secret number if the player fails after 5 attempts.  
  2. Write a small program using `rustc` only that reads two numbers from stdin and prints their product.  
  3. Explore `cargo test` by writing a test for a function that calculates the factorial of a number.

Continue to **Chapter 2** to learn basic Rust syntax, data types, and control flow!
