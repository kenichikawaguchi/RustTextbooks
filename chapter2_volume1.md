# Chapter 2: Basic Syntax & Data Types

**Goals:**  
- Learn how to declare and use variables in Rust  
- Understand mutability and its rules  
- Explore scalar and compound data types  
- Practice variable shadowing and type inference  

---

## 2.1 Variables and Mutability

In Rust, variables are immutable by default. To make a variable mutable, you must use the `mut` keyword.

```rust
fn main() {
   let x = 5;          // immutable by default
   println!("x is {}", x);

   let mut y = 10;     // mutable variable
   println!("y is {}", y);
   y = 15;
   println!("y is now {}", y);
}
```

- Attempting to reassign to an immutable variable results in a compile-time error.  
- Use `mut` when you need to change the value.

---

## 2.2 Scalar Types

Scalar types represent a single value. Rust has four primary scalar types:

1. **Integers**: `i8`, `i16`, `i32`, `i64`, `i128`, `isize` and their unsigned counterparts `u8`, `u16`, etc.  
2. **Floating-Point**: `f32`, `f64` (default).  
3. **Booleans**: `bool` with values `true` or `false`.  
4. **Characters**: `char`, representing a Unicode scalar value, e.g., `'z'`, `'ℤ'`, `'🐇'`.

Example:

```rust
fn main() {
   let a: i32 = -42;
   let b: u8 = 255;
   let c = 3.14;       // f64 by default
   let is_active: bool = true;
   let letter: char = 'A';

   println!("a = {}, b = {}, c = {}, active = {}, letter = {}", a, b, c, is_active, letter);
}
```

---

## 2.3 Compound Types

Compound types group multiple values into one type. Rust has two primitive compound types: tuples and arrays.

### Tuples

Fixed length, heterogeneous types:

```rust
fn main() {
   let tup: (i32, f64, u8) = (500, 6.4, 1);
   let (x, y, z) = tup;      // destructuring
   println!("x = {}, y = {}, z = {}", x, y, z);
   println!("First element = {}", tup.0);
}
```

### Arrays

Fixed length, homogeneous types:

```rust
fn main() {
   let arr: [i32; 4] = [1, 2, 3, 4];
   let first = arr[0];
   println!("first = {}", first);
}
```

---

## 2.4 Variable Shadowing

Rust allows you to declare a new variable with the same name as a previous variable. This is called *shadowing*.

```rust
fn main() {
   let x = 5;
   let x = x + 1;      // shadows previous x
   {
       let x = x * 2;  // shadows in inner scope
       println!("inner x = {}", x);
   }
   println!("outer x = {}", x); // the first shadowed x
}
```

- Shadowing is different from mutability: you can change the type when shadowing.

---

## 2.5 Basic Operations and Type Inference

Rust can infer types in many cases:

```rust
fn main() {
   let sum = 5 + 10;            // inferred as i32
   let difference = 95.5 - 4.3; // f64 by default
   let product = 4 * 30;
   let quotient = 56.7 / 32.2;
   let remainder = 43 % 5;

   println!(
       "sum = {}, diff = {}, prod = {}, quot = {}, rem = {}", 
       sum, difference, product, quotient, remainder
   );
}
```

- Use explicit type annotations when needed for clarity or when types cannot be inferred.

---

## Exercises

1. Declare an immutable variable `z` with value `100`, then try to modify it. Observe the compiler error and then fix it using `mut`.  
2. Create a tuple with your name, age, and a boolean indicating student status. Destructure and print each value.  
3. Define an array of five floating-point numbers, and print the third element.  
4. Experiment with shadowing: declare `let spaces = "   ";` then shadow it with `let spaces = spaces.len();`. Print both.  
5. Write a small function that takes two `i32` parameters and returns a tuple `(sum, product)`. Test it in `main()`.  
