- "Function types are more useful if they're OK with their arguments being less useful."
- constrast: variance of argument types on their own with their variance when used as function arguments...

```rust
let x: &'static str; // more useful, lives longer
let x: &'a str;      // less useful, lives shorter

fn take_func1(&'static str) // stricter, so less useful
fn take_func2(&'a str)      // less strict, more useful
```

- `Fn(T)` is contravariant in `T`