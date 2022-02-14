- if you move a value behind a mutable reference, then **you must leave a value in its place, so that the [[I.D.1. owner]] has a value to drop**
		- code below shows two methods from std::mem that help us achieve the above
		- `std::mem::take`
		- `std::mem::swap`

```rust
fn replace_with_84(s: &mut Box<i32>) {

    // let was = *s; // This is an example of trying to move a value behind a mutable reference. We CANNOT do this because then *s would be empty.
	// std::mem::take is one way to move a value while replacing s with it's `Default` value (default Box<i32> is pointer to `0` on the heap).

	// example of std::mem::take
	let was = std::mem::take(s); // instead of let was = *s;
	*s = was;                    // we can still move a value back into s
    // (at this point, s is a box of 42 again, nothing changed)

	// std::mem::swap is another way to move a value, it lets us swap values at two mutable locations
	// example of std::mem::swap
	let mut r = Box::new(84);
	std::mem::swap(s, &mut r); // swap values behind s and r (Box of 42 & Box of 84)
	assert_ne!(*r, 84); // *r is Box of 42 now, and s is Box of 84 now
}

let mut s = Box::new(42);
replace_with_84(&mut s);
```

`std::mem::take` is equivalent to `std::mem::replace(&mut value, Default::default())`

Help:
- In the book, what is (3) trying to say?
- https://rust-dc.zulipchat.com/#narrow/stream/312937-book-club/topic/Ch.201.20Help.20-.20Confusion.20on.20Page.2011.2C.20Listing.201-7.2C.20Number.203


QUESTION:
- mem::replace
	- Why use this instead of `*dest = src` ?