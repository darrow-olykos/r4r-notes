What:
- Pool of memory that is not tied to current call stack
- Contains values that live until they are explicity deallocated (free'ed)
- Allows you to allocate contiguous segments of memory w/ pointer at start of segment
- In heap-allocated memory, resulting pointer has unconstrianed lifetime

How:
- use `Box<T>`!
	- `Box::new(value)` allocates on heap, returns a `Box<T>` which is a pointer to that value
	- memory is freed when the `Box` is dropped

Risk:
- [[III.A.2.i. leaking memory]]

Why:
- For when you want a value to live beyond the lifetime of the current function's frame (e.g. send to another thread)