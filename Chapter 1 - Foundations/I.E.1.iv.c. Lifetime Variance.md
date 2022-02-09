## Why
- Why do we need to learn about variance when it comes to lifetimes?
		- Variance becomes relevant when you consider how geneirc lifetime parameters interact with the borrow checker.

## What
- variants are like subtypes, e.g. `&'static str` is valid to pass to a function that accepts a `&'a str` 
- three types of variance:
	- [[I.E.1.iv.d. covariant]]
	- [[I.E.1.iv.e. invariant]]
	- [[I.E.1.iv.f contravariant]]

```rust
struct MutStr<'a, 'b> {
	s: &'a mut &'b str
}
let mut s = "hello";
&MutStr { s: &mut s }.s = "world";
println!("{}", s);
```