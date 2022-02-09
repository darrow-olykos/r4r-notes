-  a type is **covariant** if you can just use a subtype in place of the type
- `&'static T` can be provided to something expecting `&'a T`
		- "`&'a T` is **covariant** in `'a'`"
	- `&Vec<&'static str>` can be provided to something expecting `'a T`
			- "`&'a T`" is also **covariant** in `T`"
- see also: [[I.E.1.iv.e. invariant]] and [[I.E.1.iv.f contravariant]]