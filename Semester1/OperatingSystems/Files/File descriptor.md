File descriptor is like an index (non-negative `int`) of the created data structure in the OS core. There are system information about the file and it's flags, check full list of flags here `man 2 open` or here `man 2 fcntl`.

Max value of file descriptor is less than `OPEN_MAX`-1 (limit of opened files at a time). `OPEN_MAX` has "soft" and "hard" [[Limits]].