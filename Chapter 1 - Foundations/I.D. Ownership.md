- The main idea:
	- all values have a single [[I.D.1. owner]], enforced by the Borrow Checker
	- if a value is moved, the ownership of the value moves from the old location to the new one & you can no longer access the moved value through [[I.A.4. variable]]s that [[I.B.1.i. flows]] from the original [[I.D.1. owner]]

- Exceptions to this rule:
	- types that implement [[I.D.2. Copy trait]]

