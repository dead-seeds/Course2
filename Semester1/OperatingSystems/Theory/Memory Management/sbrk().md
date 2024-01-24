`void *sbrk(intptr_t increment)`

`brk()` and  `sbrk()` change the location of the program break, which defines the end of the process's data segment (the program break is the first location after the end of the uninitialized data segment). Increasing the program break has the effect of allocating memory to the process, decreasing the break deallocates memory. Calling `sbrk()` with an increment of 0 can be used to find the current  location of the program break.

The `sbrk()` system call moves the "border" of the data segment. This means it moves a border of an area in which a program may read/write data (letting it grow or shrink, although AFAIK no [[malloc()]] really gives memory segments back to the [[Kernel]] with that method). Aside from that, there's also `mmap` which is used to map files into memory but is also used to allocate memory (if you need to allocate shared memory (check [[Virtual memory]]), `mmap` is how you do it).

On success, `brk()` returns zero.  On error, -1 is returned, and [[errno]] is set to `ENOMEM`.