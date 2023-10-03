<<<<<<< HEAD
<<<<<<< HEAD:Semester1/OperatingSystems/Files and catalogues/File descriptor.md
File descriptor is like an index (non-negative `int`) of the created data structure in the [[OS]] core. The table of file descriptors is stored in user process part of [[Virtual memory]], but the structures, that describe files are stored in shared object part. 
=======
File descriptor is like an index (non-negative `int`) of the created data structure in the OS core. The table of file descriptors is stored in each user process part of [[Virtual memory]], but the structures, that describe files are stored in shared object part.
>>>>>>> 52db4bb (Clafifications from previous lecture):Semester1/OperatingSystems/Files/File descriptor.md

Table of file descriptors contain pointers to file descriptor objects that in consequently contain:
=======
File descriptor is like an index (non-negative `int`) of the created data structure in the OS core. The table of file descriptors is stored in each user process part of [[Virtual memory]], but the structures, that describe files are stored in shared object part.

<<<<<<< HEAD
Table of file descriptors contain pointers to file objects that in consequently contain:
>>>>>>> fc2c424 (Directories permissions + notes from two lectures (#6))
=======
Table of file descriptors contain pointers to file descriptor objects that in consequently contain:
>>>>>>> be7dfd4 (Start of dynamic memory management, good + bad source to find information, file clarifications)
* Current offset in opened file.
* Flags.
* Counter of pointers to this file description.
* Pointer to [[inode]].
If you open file N times, there will be N file structures.
Actually, file will be closed only if it will be closed in parent process and all sub-processes.

Max value of file descriptor is less than `OPEN_MAX`-1 (limit of opened files at a time). `OPEN_MAX` has "soft" and "hard" [[Limits]].