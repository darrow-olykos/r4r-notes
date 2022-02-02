What:
- aka a "stack frame"
- a contiguous chunk of memory that is allocated at the top of [[III.A.1. The Stack]] each time a function is called
- contains all the variables within that function, along with any arguments the function takes
- closely tied to notion of lifetimes: references to a variable must have a lifetime that is ***at most*** as long as the lifetime of the frame, because variable stored in a frame on the stack cannot be accessed after that frame goes away