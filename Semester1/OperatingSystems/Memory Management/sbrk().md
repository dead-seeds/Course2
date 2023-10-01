`void *sbrk(intptr_t increment)`

`brk()` and  `sbrk()` change the location of the program break, which defines the end of the process's data segment (the program break is the first location after the end of the uninitialized data segment). Increasing the program break has the effect of allocating memory to the process, decreasing the break deallocates memory. Calling `sbrk()` with an increment of 0 can be used to find the current  location of the program break.

On success, `brk()` returns zero.  On error, -1 is returned, and [[errno]] is set to `ENOMEM`.