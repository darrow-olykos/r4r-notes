- https://doc.rust-lang.org/std/marker/trait.Copy.html
- assignment copies value, so both old and new location remain accessible (exception to Rust's main idea of [[I.D. Ownership]])
- most Rust primitives implement this by default
- to be `Copy`, a type must not contain non-copy types as well as any type that owns a resource it must deallocate when the value is dropped

```rust
fn main() {
    let x1 = 42;
    let y1 = Box::new(84);
    {   // start new scope
    	let z = (x1, y1);
        // z goes out of scope and thus is dropped (and in turn drops values in x1 and x2)
    }
    let x2 = x1;
    println!("{x2}"); // this is OK, x1 implements Copy, and was not moved into z.
    // println!("{y1}"); // this would error, since y1 was moved into z. y1 does not implement Copy
}
```
