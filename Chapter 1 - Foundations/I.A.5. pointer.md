What
- a [[I.A.1. value]] that holds the <u>address of a region of memory</u>, so the pointer "points to a [[I.A.3. place]]"
- can be dereferenced to access the [[I.A.1. value]] stored in <u>the memory location</u> that it points to
- the same pointer can be stored in multiple different [[I.A.4. variable]]s (multiple variables can have the same pointer value)

```rust

let x = 42;        // 42 is a value (not a pointer)
let y = 43;        // 43 is a value (not a pointer)
let var1 = &x;     // the address of x is a value (pointer)
let mut var2 = &x; // the address of x is a value (pointer) (var1 and var2 hold two different copies of the same value)
var2 = &y;         // the address of y is a value (pointer)...
                   // ...changing value in var2 does not change value in var1

```

```rust
let s = "Hello, Universe";

// s is a variable
// the value of s is a pointer to the first character in the string value "Hello, Universe";

// ...value technically includes length of string, "wide pointer types" will be discussed in Chapter 2
```