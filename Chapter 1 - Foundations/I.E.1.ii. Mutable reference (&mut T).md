- `&mut T`
- mutable references differ from [[I.E.1.i. Shared reference (&T)]] in that mutable reference is **exclusive**:
	- 1. Assumes that no other threads are accessing the target value 
	- 2. Lets you mutate the ***memory location*** that the reference points to
	- 3. "Whether you can mutate the values that lie beyond the immediate reference is dependent on the type that lies between"

```rust
fn noalias(input: &i32, output: &mut i32) {
	// rust compiler can assume `input` and `output` do not point to the same memory
	if *input = 1 {
		*output = 2; // therefore, this re-assignment..
	}
	if *input != 1 { // ...cannot impact this check
		*output = 3;
	}
}
```

```rust
let x = 42;
let mut y = &x; // y is of type &i32
let z = &mut y; // z is of type &mut &i32
```

```rust

fn main() {
    let a = 42;      // a is of type i32
    // a = 43;       // cannot re-assign variable a, it is immutable
    
    let b = &a;      // b is of type &i32 (shared reference)
    println!("{b}"); // => 42
    // *b = 44;      // cannot change underlying value of a, a is immutable (and we did not mutably borrow from a)
    // b = 44;       // cannot re-assign variable b, b is immutable
    
    let mut z = &a;  // z is of type &i32 (shared reference), z is mutable
    z = &45;         // z can be re-assigned since z is mut
    println!("{z}"); // => 45
    println!("{a}"); // => 42
                     // a is unchanged since it was the value of z that was changed, not the value that z was "pointing" at
    
    let mut c = &a; // c is of type &i32 (shared reference), c is mutable, we immutably borrow from a
    let d = &mut c; // d is of type &mut &i32 (we mutably borrowed from c. c is mutable, it points to a shared reference of a type i32)
    //**d = 47;     // we CANNOT change the value lying beyond the shared reference, (c does not mutably borrow a AND a is not mutably borrowable)
    *d = &46;       // we can change the shared reference, like we did with the `z` example
    
    println!("{d}"); // => 46
    println!("{a}"); // => 42
    change_value_through_mutable_reference(); // example
}

fn change_value_through_mutable_reference() {
    let mut a = 42;      // a is mutable (which means it is mutably borrowable)
    let b = &mut a;      // &a would be an immutable borrow, &mut a is a mutable borrow
    *b = 43;             // dereference b to mutate value that a contains, this works because 1. a is mut AND 2. b mutably borrowed from a
    println!("{b}");     // => 43
}

```

- Difference between [[I.D. Ownership]] and mutable reference?
		- the [[I.D.1. owner]] is responsible for dropping the [[I.A.1. value]] when it is no longer necessary
		- everything else is the same except for when you [[I.E.1.ii.a. Move a value behind a mutable reference]]
