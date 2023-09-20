File descriptor is like an index (non-negative `int`) of the created data structure in the OS core. The table of file descriptors is stored in user process part of [[Virtual memory]], but the structures, that describe files are stored in shared object part. 

This structure has:
* Current offset in opened file.
* Flags.
* Counter of pointers to this file description.
* Pointer to [[inode]].


Max value of file descriptor is less than `OPEN_MAX`-1 (limit of opened files at a time). `OPEN_MAX` has "soft" and "hard" [[Limits]].