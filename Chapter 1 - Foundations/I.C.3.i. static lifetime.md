- `'static`  lifetime marks a reference as being valid for "as long as static memory is around", which is until program shuts down
- *"there can be `'static` references that do not point to static memory, but it might as well be in static memory as far as the rest of the program is concerned, as it can be used for however long your program wishes"*


 **a bound like `T: 'static`** 
- indicates that the type param `T` is able to live for however long we keep it around for, up to and including the remaining execution of the program.
- requires that `T` is `owned` and self-sufficient
	- either:
		- does not does not borrow other non-static values OR
		- anything that it does borrow is also `'static` (and thus will stick around until the end of the program)
	- Example: `std::thread::spawn`

