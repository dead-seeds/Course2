`void free(void *ptr)`
`free` frees memory with labeling it as free, like "can be reused". Then `malloc` or `calloc` or `realloc` can take these bytes chunks.
If `ptr` has already been freed, undefined behavior occurs.