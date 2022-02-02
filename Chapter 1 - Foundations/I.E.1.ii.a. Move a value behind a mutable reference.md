```rust
fn replace_with_84(s: &mut Box<i32>) {
	let was = std::mem::take(s);
	*s = was;
	let mut r = Box::new(84);
	std::mem::swap(s, &mut r);
	assert_ne!(*r, 84);
}

let mut s = Box::new(42);
replace_with_84(&mut s);
// TODO - comment
```