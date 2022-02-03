- types that allow you to mutate a value through a [[I.E.1.i. Shared reference (&T)]].
- usually rely on additional mechanisms (atomic CPU instructions or invariants)
- two categories:
	- 1. Those that let you get a [[I.E.1.ii. Mutable reference (&mut T)]] through a [[I.E.1.i. Shared reference (&T)]]
			- `Mutex`
			- `RefCell`
			- ensures that for any value they give a mutable reference to, only one mutable ref (and no shared refs) exists at a time
			- under the hood, depends on `UnsafeCell` (discussed in Chapter 9, it is the _only_ correct way to mutate thru a [[I.E.1.i. Shared reference (&T)]])
	- 2. Those that let you replace a [[I.A.1. value]] given a [[I.E.1.i. Shared reference (&T)]]
				- `std::sync::atomic` integers
				- `std::cell::Cell` [[I.E.1.iii.a. Cell type]]
			- these types give you methods for manipulating that value rather than handing out a [[I.E.1.ii. Mutable reference (&mut T)]]