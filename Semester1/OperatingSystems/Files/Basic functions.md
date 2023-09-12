
# open()
`open(const char *pathname, int flags)`

Function call returns [[File descriptor]].
There are only three possible options: `O_RDONLY`, `O_WRONLY`, or `O_RDWR`. These request opening the file read-only, write-only, or read/write.

If we create a new file with `open(const char *pathname, int flags, mode_t mode)` , `mode` sets [[File permissions]] (number like in `chmod`) to this file. There are a lot of creation `flags`, check `man 2 open`. 


# read()
`read(int fd, void *buffer, size_t n)`

The function reads less or equal to `n` bytes from the file. Function call returns number of red bytes in `ssize_t` format (in early UNIX versions was `int` ("Haviland - System programming", page 31), but `int` can change it's size in the future, so `ssize_t` type was created). If we can use `lseek` (make shifts), `offset` (our shift from the file beginning) is increased by number of bytes we've red. If `offset` is already at the `EOF`, `read` gets 0 bytes and returns 0. Reading less than `n` bytes is not an error, so you better check the number of bytes that were red and compare to what you expect.

`read()` is one of the low-level bricks in I/O system that is used by `scanf()` and other high-level tools.

System tracks the position in the file with the object called `read-write pointer` or just `file pointer`. (but r/w pointer is more correct I think)


# write()
`write(int filedes, const void *buffer, size_t n)`

`write` copies data from buffer (like it's an array of bytes) to the file referred to by the `filedes`. On success, the number of bytes written is returned. On error, -1 is returned, and `errno` is set to indicate the error.


# close()
`close(int fd)`

OMG, `close` closes the [[File descriptor]] (it no longer refers to any file description) and it can be reused. [[File permissions]], that process had, removes. If this is the last `fd` of connected file description, resources are freed.

`close()` returns 0 on success and -1 on error (`errno` is set to indicate the error).


# lseek()
`off_t lseek(int fd, off_t offset, int whence)`

Reposition read/write file offset according to the directive `whence`.

`WHENCE`:	
	`SEEK_SET`
        The file offset is set to offset bytes.
	`SEEK_CUR`
	    The  file  offset  is  set  to  its current location plus offset bytes.
	`SEEK_END`
        The file offset is set to the  size  of  the  file  plus  offset bytes.