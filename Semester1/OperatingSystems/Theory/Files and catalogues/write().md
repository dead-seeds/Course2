`write(int filedes, const void *buffer, size_t n)`

`write` copies data from buffer (like it's an array of bytes) to the standard buffer with size of `BUFSIZE` and then to the file referred to by the `filedes`. On success, the number of bytes written is returned. On error, -1 is returned, and [[errno]] is set to indicate the error.

It can block if device or intermediate buffer is out of memory.