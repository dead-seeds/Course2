`off_t lseek(int fd, off_t offset, int whence)`

Reposition read/write file offset according to the directive `whence`.

`WHENCE`:	
	`SEEK_SET`
        The file offset is set to offset bytes.
	`SEEK_CUR`
	    The file offset is set to its current location plus offset bytes.
	`SEEK_END`
        The file offset is set to the size of the file plus offset bytes.