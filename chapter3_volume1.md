# Chapter 3: Control Flow

**Goals:**  
- Understand Rust’s control flow constructs (`if`, `loop`, `while`, `for`)  
- Learn pattern matching with `match`  
- Write programs that branch and repeat logic  

---

## 3.1 `if` Expressions

Rust’s `if` is an expression, meaning it returns a value.

```rust
fn main() {
   let number = 7;

   if number < 5 {
       println!("{} is less than 5", number);
   } else {
       println!("{} is greater than or equal to 5", number);
   }

   // `if` as an expression
   let parity = if number % 2 == 0 {
       "even"
   } else {
       "odd"
   };
   println!("{} is {}", number, parity);
}
```

- Conditions must evaluate to a `bool`.  
- Both branches of an `if` expression must return the same type.

---

## 3.2 `loop`

Infinite loops that you can break out of explicitly.

```rust
fn main() {
   let mut count = 0;
   loop {
       count += 1;
       println!("Count = {}", count);
       if count == 5 {
           println!("Reached 5, breaking out");
           break;
       }
   }
}
```

- Use `break` to exit.  
- You can return a value from a `loop`:

```rust
fn main() {
   let mut count = 0;
   let result = loop {
       count += 1;
       if count == 10 {
           break count * 2;
       }
   };
   println!("Result: {}", result);
}
```

---

## 3.3 `while`

Conditional loops that run while a condition is true.

```rust
fn main() {
   let mut n = 3;
   while n != 0 {
       println!("{}!", n);
       n -= 1;
   }
   println!("LIFTOFF!!!");
}
```

- Check the condition before each iteration.  
- Useful for looping until a particular state is reached.

---

## 3.4 `for` Loops

Iterate over an iterator or range.

```rust
fn main() {
   // Range
   for i in 1..=5 {
       println!("{}", i);
   }

   // Array iteration
   let arr = [10, 20, 30, 40];
   for &value in arr.iter() {
       println!("Value = {}", value);
   }
}
```

- `1..=5` is inclusive; `1..5` is half-open.  
- Iterators are lazy and powerful (`map`, `filter`, etc.).

---

## 3.5 `match` and Pattern Matching

`match` allows branching on many patterns.

```rust
enum Direction {
   Up,
   Down,
   Left,
   Right,
}

fn main() {
   let dir = Direction::Left;

   match dir {
       Direction::Up => println!("Going up!"),
       Direction::Down => println!("Going down!"),
       Direction::Left => println!("Going left!"),
       Direction::Right => println!("Going right!"),
   }

   // Matching values
   let x = 2;
   match x {
       1 => println!("One"),
       2 | 3 => println!("Two or three"),
       4..=6 => println!("Between four and six"),
       _ => println!("Something else"),
   }
}
```

- Patterns can include literals, ranges, enums, and more.  
- The `_` wildcard catches all other cases.  
- `if let` for concise matching:

```rust
let some_option = Some(5);
if let Some(value) = some_option {
   println!("Got {}", value);
} else {
   println!("None");
}
```

---

## Exercises

1. Write a function that takes an integer and returns `"positive"`, `"negative"`, or `"zero"` using `if`.  
2. Use a `loop` to calculate the factorial of 5, returning the result from the loop.  
3. Rewrite the factorial with a `while` loop.  
4. Create a vector of strings and use a `for` loop to print each element’s length.  
5. Define an `enum` for `Coin` with variants `Penny`, `Nickel`, `Dime`, `Quarter`, then write a `match` to return its value in cents.
