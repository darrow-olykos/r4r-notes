- failing to deallocate heap memory can result in leaking memory, which can eat up all memory on your machine
- there are SOME cases where we want to do this intentionally:
	-If you want to get a `'static` reference, you can use `Box::leak` (Let's us dynamically obtain a `'static` reference after program starts)
