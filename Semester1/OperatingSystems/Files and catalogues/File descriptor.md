File descriptor is like an index (non-negative `int`) of the created data structure in the [[OS]] core. The table of file descriptors is stored in user process part of [[Virtual memory]], but the structures, that describe files are stored in shared object part. 

Table of file descriptors contain pointers to file descriptor objects (file description) that in consequently contain:
* Current offset in opened file.
* Flags.
* Counter of pointers (file descriptors) to this file description.
* Pointer to [[inode]].
For more details on file descriptions see `man 2 open` section NOTES.
> 	You can look at the file descriptor table of any open running process by running `lsof -p PID` with [[PID]] of interesting process. However, this does not work on Solaris (probably because of some permissions issues)

If you open file N times, there will be N file structures.
Actually, file will be closed only if it will be closed in parent process and all sub-processes.

Max value of file descriptor is less than `OPEN_MAX`-1 (limit of opened files at a time). `OPEN_MAX` has "soft" and "hard" [[Limits]].