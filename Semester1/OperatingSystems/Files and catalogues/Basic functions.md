Standard `stdio` I/O functions optimize the number of [[System call]]s with bufferization.

All read/write with `stdio` functions works through buffer system. It means that library functions transfer data from user's buffer to the secondary buffer. Then `wirte(2)` writes bytes from secondary buffer with size `BUFSIZ` to the system buffer, bytes from the system buffer finally reach I/O device. Same situation with `read(2)`: data from device -> system buffer -> user's buffer.

You can use `setbuf(3S)` to change bufferization mode or turn it off.