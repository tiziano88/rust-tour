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
@[7-8](Invalid array element access `thread '<main>' panicked at 'index out of bounds: the len is 5 but the index is 10'`)

---

```
$ cargo run
   Compiling arrays v0.1.0 (file:///projects/arrays)
     Running `target/debug/arrays`
thread '<main>' panicked at 'index out of bounds: the len is 5 but the index is
 10', src/main.rs:6
note: Run with `RUST_BACKTRACE=1` for a backtrace.
```

---

# How Functions Work

---

# Comments

---

# Control Flow
