# Rust Tour

---

### Variables and Mutability

Variables are _immutable_ by default

```rust
fn main() {
    let x = 5;
    println!("The value of x is: {}", x);
    x = 6;
    println!("The value of x is: {}", x);
}
```

```
error[E0384]: re-assignment of immutable variable `x`
 --> src/main.rs:4:5
  |
2 |     let x = 5;
  |         - first assignment to `x`
3 |     println!("The value of x is: {}", x);
4 |     x = 6;
  |     ^^^^^ re-assignment of immutable variable
```

---

### Variables and Mutability

Variables can be declared as mutable with the `mut` keyword

```rust
fn main() {
    let mut x = 5;
    println!("The value of x is: {}", x);
    x = 6;
    println!("The value of x is: {}", x);
}
```

```
$ cargo run
   Compiling variables v0.1.0 (file:///projects/variables)
     Running `target/debug/variables`
The value of x is: 5
The value of x is: 6
```

---

### Constants

- Declared with the `const` keyword
- _Must_ be annotated with their type
- Can be declared in any scope, including the global scope
- Valid for the entire time a program runs, within the scope they were declared
  in

```rust
const MAX_POINTS: u32 = 100_000;
```

---

### Shadowing

- Can declare a new variable with the same name as a previous variable

```rust
fn main() {
    let x = 5;
    let x = x + 1;
    let x = x * 2;
    println!("The value of x is: {}", x);
}
```

```
$ cargo run
   Compiling variables v0.1.0 (file:///projects/variables)
     Running `target/debug/variables`
The value of x is: 12
```

---

## Data Types

- Statically typed (all types known at compile time)
- Compiler can _infer_ types

---

### Scalar Types

- integers
- floating-point numbers
- booleans
- characters

---

### Integer Types

Length | Signed | Unsigned
-------|--------|---------
8-bit  |`i8`    |`u8`
16-bit |`i16`   |`u16`
32-bit |`i32`   |`u32`
64-bit |`i64`   |`u64`
arch   |`isize` |`usize`

---

### Integer Literals

Number Literals  | Example
-----------------|--------------
Decimal          | `98_222`
Hex              | `0xff`
Octal            | `0o77`
Binary           | `0b1111_0000`
Byte (`u8` only) | `b'A'`

---

### Floating-Point Types

`f32` and `f64`

### Boolean Type

`bool`

`true` and `false`

### Character Type

`char`

---

## Compound Types

### Tuple

```rust
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);

    let (x, y, z) = tup;
    println!("The value of y is: {}", y);

    let five_hundred = x.0;
    let six_point_four = x.1;
    let one = x.2;
}
```

@[2](Creation)
@[4-5](Pattern Matching)
@[7-9](Accessors)

---

## Arrays

```rust
fn main() {
    let a = [1, 2, 3, 4, 5];

    let first = a[0];
    let second = a[1];

    let index = 10;
    let element = a[index];
}
```

@[2](Creation)
@[4-5](Accessing elements)
@[7-8](Invalid array element access: `thread '<main>' panicked at 'index out of bounds: the len is 5 but the index is 10'`)

---

### How Functions Work

```rust
fn main() {
    another_function(5, 6);
}

fn another_function(x: i32, y: i32) {
    println!("The value of x is: {}", x);
    println!("The value of y is: {}", y);
}
```

---

### Statements and Expressions

- _Statements_
  - Instructions that perform some action and do not return a value
- _Expressions_
  - Evaluate to a resulting value
  - Do not include ending semicolon

---

### Return Values

The return value of a function is the value of the final expression in the block
of the body.

```rust
fn main() {
    let x = plus_one(5);

    println!("The value of x is: {}", x);
}

fn plus_one(x: i32) -> i32 {
    x + 1
}
```

---

```rust
fn main() {
    let x = plus_one(5);

    println!("The value of x is: {}", x);
}

fn plus_one(x: i32) -> i32 {
    x + 1;
}
```

```
error[E0308]: mismatched types
 --> src/main.rs:7:28
  |
7 |   fn plus_one(x: i32) -> i32 {
  |  ____________________________^
8 | |     x + 1;
9 | | }
  | |_^ expected i32, found ()
  |
  = note: expected type `i32`
             found type `()`
help: consider removing this semicolon:
 --> src/main.rs:8:10
  |
8 |     x + 1;
  |          ^
```

---

## Comments

```rust
// I am a comment.
let lucky_number = 7; // Me too.
```

---

## Control Flow

### `if` expressions

```rust
fn main() {
    let condition = true;
    let number = if condition {
        5
    } else {
        6
    };

    println!("The value of number is: {}", number);
}
```

---

### `loop`

```rust
fn main() {
    loop {
        println!("again!");
    }
}
```

---

### `while`

```rust
fn main() {
    let mut number = 3;

    while number != 0 {
        println!("{}!", number);

        number = number - 1;
    }

    println!("LIFTOFF!!!");
}
```

---

### `for`

```rust
fn main() {
    let a = [10, 20, 30, 40, 50];

    for element in a.iter() {
        println!("the value is: {}", element);
    }
}
```

---

## Exercise

Create a map from strings to string and print it out in JSON format.

Expected output:

```json
{
  "Italy": "London",
  "France": "Paris",
  "United Kingdom", "London"
}
```

+++

### Solution

```rust
use std::collections::HashMap;

fn main() {
    let mut entries: HashMap<String, String> = HashMap::new();
    entries.insert("foo".to_string(), "bar".to_string());
    entries.insert("test".to_string(), "nnn".to_string());

    println!("{{");
    for (i, (k, v)) in entries.iter().enumerate() {
        let trail = if i < entries.len() - 1 { "," } else { "" };
        println!("  {}: {}{}", k, v, trail);
    }
    println!("}}");
}
```
