- whenever a [[I.E.1. reference]] with some lifetime `'a` is used, the compiler checks that the [[I.B.1.i. flow]] of the reference we are accessing does not conflict with any other parallel [[I.B.1.i. flow]]s.

```rust
let mut x = Box::new(42);
let r = &x;               // 'a - lifetime starts

if rand() > 0.5 {
	*x = 84;              // r lifetime does not exist in this branch
						  // , even though r is technically "in scope"
} else {
	println!("{}", r);   // 'a - r lifetime exists here because r is being used
}
// r goes out of scope here

// NOTE:
// println!("new use: {}", r); // this would cause compile error
//  the key rule is: You cannot mutate a value that is being used by shared references, so adding another use of r here means we are potentially using a reference to &x after its value is mutated in the first branch *x = 84;
```

