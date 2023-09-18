`void *malloc(size_t size)`

If the size of the space requested is zero, the behavior is implementation-defined: either a null pointer is returned to indicate an error, or the behavior is as if the size were some nonzero value.

Source code: https://codebrowser.dev/glibc/glibc/malloc/malloc.c.html
