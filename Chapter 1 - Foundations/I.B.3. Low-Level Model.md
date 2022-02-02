Compare to [[I.B.1. High-Level Model]]

```rust
  let x: usize;
```
- *"the variable `x` is a name for a region of memory on the stack that has room for a value the size of `usize`."*

What:
- [[I.A.4. variable]] is a name to a memory location
- [[I.A.4. variable]] is a "[[I.A.1. value]] slot"
- assigning: a [[I.A.1. value]] fills the slot w/ new [[I.A.1. value]] and drops the old one
- access: compiler checks if slot is empty (unintialized or moved)
- [[I.B.2. shadowing]] variables results in different chunks of memory backing them (matches C/C++ model)

NOTE: compiler may use CPU register to back a value instead of region of memory