What:
- [[II.A.1. High-Level Model]] for tracing the lifetime of a particular instance of a [[I.A.1. value]]
- can fork and merge when there are branches, with each split tracing a distinct lifetime for that [[I.A.1. value]]
- compiler can enforce rules like *"there cannot be two parallel **flows** with mutable access to a [[I.A.1. value]]"

```rust

// this code does not compiler (the borrow checker rejects it)

let mut x;

x = 42;             // vertex (1)

let y = &x;         // vertex (2)

x = 43;             // vertex (3) exclusive &mut flow from (1) to here

assert_eq!(*y, 42); // vertex (4) shared (&) flow from (1) through (2) to here

```

In terms of flows:
```

               +-------+
               | (1)   +-----------+
               ++------+           |
                |                  |
                |                  |
          shared flow (&)     exclusive flow (&mut)
                |                  |
                |                  |
               ++------+           |
      +--------+ (2)   |           |
      |        +-------+           |
      |                            |
      |                            |
  shared flow (&)                  |
      |                            |
      |        +-------+           |
   -> |        | (3)   +-----------+ <- Borrow checker rejects code since we cannot
      |        +-------+                  have both a shared use and excl flow concurrently ***
      |                                   (if 4 didn't exist, there would be no conflict)
      |
      |
      |
      |        +-------+
      +--------+ (4)   |
               +-------+


```

In terms of "borrowing" and [[I.A.1. value]]s:
You can't assign a value that was borrowed IF that borrowed value is used later.
	1. `y` borrowed from `x` at (2)
	2. `x` was assigned a new value at (3)
	3. borrowed value used at (4)