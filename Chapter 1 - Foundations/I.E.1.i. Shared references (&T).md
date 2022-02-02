- `&T`
- a pointer that may be shared
- each shared reference is a `Copy`
- [[I.A.1. value]]s behind shared references are immutable

Should never fail:
```rust
fn cache(input: &i32, sum: &mut i32) {
	*sum = *input + *input;
	assert_eq!(*sum, 2 * *input);
}
```

Interesting notes:
- *"Rust compiler is allowed to assume the value a shared reference points to **will not change** while that reference lives...if compiler sees value behind shared reference is read multiple times in a function, it is within its rights to read it only once and reuse that value."*
- *"Compiler heuristics change over time, so you generally want to code against the compiler is allowed to do, rather than what it actually does in a particular case at a particular moment in time"*
