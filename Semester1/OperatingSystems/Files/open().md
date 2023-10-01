	 g`open(const char *pathname, int flags)`

Function call returns [[File descriptor]].
There are only three possible options: `O_RDONLY`, `O_WRONLY`, or `O_RDWR`. These request opening the file read-only, write-only, or read/write.

If we create a new file with `open(const char *pathname, int flags, mode_t mode)` , `mode` sets [[File permissions]] (number like in `chmod`) to this file. There are a lot of creation `flags`, check `man 2 open`.