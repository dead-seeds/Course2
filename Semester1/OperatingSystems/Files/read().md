`read(int fd, void *buffer, size_t n)`

The function reads less or equal to `n` bytes from the file. Function call returns number of red bytes in `ssize_t` format (in early UNIX versions was `int` ("Haviland - System programming", page 31), but `int` can change it's size in the future, so `ssize_t` type was created). If we can use `lseek` (make shifts), `offset` (our shift from the file beginning) is increased by number of bytes we've red. If `offset` is already at the `EOF`, `read` gets 0 bytes and returns 0. Reading less than `n` bytes is not an error, so you better check the number of bytes that were red and compare to what you expect.

`read()` is one of the low-level bricks in I/O system that is used by `scanf()` and other high-level tools.

System tracks the position in the file with the object called `read-write pointer` or just `file pointer`. (but r/w pointer is more correct I think)