## The Result Enum

Enums are powerful and useful features in Rust. This is partly due to the pattern-matching mechanism that enables exhaustive utilization of all possible values of an Enum type. One particularly useful enum is the in-built Result enum which is applicable where you want to get the result of some operation that may throw an error.

The Result Enum wraps two values; the Ok(T) and Err(E) where T and E are the expected values and error respectively. This provide a much cleaner way of handling errors.

Below are code samples that explores two main benefits of this:

1. Error composition
2. Type Safety

In Rust, if we have multiple different operation that returns the Result type, these operations are easily chaninable in a concise way. For instance, let's say we have three operations; `p_int`, `calculate_square` and `mult_by_3`. If each of these return a `Result` type, they are nicely invoked like this

```rust
fn main() {
    let num = 34;

    let result = p_int(34)
    .and_then(calculate_square)
    .and_then(mult_by_3)


    match result {
        Ok(val) => println!("{}", val),
        Err(e) => eprintln!("{}", e)
    }
}

```
