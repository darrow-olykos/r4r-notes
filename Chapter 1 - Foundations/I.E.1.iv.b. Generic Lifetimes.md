- We can make type definitions generic over one or more [[I.E.1.iv Lifetime]].
- Two subtleties:
	1. if your type also implements `Drop` then dropping your type counts as a use of any [[I.E.1.iv Lifetime]] or type your type is generic over.
			- When an instance of your type is dropped, the borrow checker will check that it's still legal to use any of your type's generic [[I.E.1.iv Lifetime]]s before dropping it. (In case your drop code DOES use any of those [[I.E.1. reference]]s)
			- If your type does not implement `Drop`, then dropping the type does not count as a use and users are free to ignore any [[I.E.1. reference]]s stored in your type as long as they do not use it anymore.
			- rules around dropping covered more in Chapter 9.
	2. Avoid making a type generic over multiple [[I.E.1.iv Lifetime]]s unless you absolutely need to.

Clarify: What does "USE OF A LIFETIME" mean?


```rust
struct StrSplit<'s, 'p> {
	delimiter: &'p str,
    document: &'s str
}

impl<'s, 'p> Iterator for StrSplit<'s, 'p> {
	type Item = &'s str;
	fn next(&self) -> Option<Self::Item> {
		todo!()
	}
}

fn str_before(s: &str, c: char) -> Option<&str> {
	StrSplit { document: s, delimiter: &c.toString() }.next()
	// .next() returns reference into the document,
    // &c.toString() is local to this function so it needed a different lifetime
}
```

