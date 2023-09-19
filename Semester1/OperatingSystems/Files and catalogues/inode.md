(In solaris it's `vnode`)
Each [[File]] has this structure that contains metadata. The following is a list of the information typically found in, or associated with, the file `inode`, with the names of the corresponding structure fields returned by `stat(2)` and `statx(2)`:
* Device where `inode` resides.
* Unique `inode` number.
* File type and mode.
* Link count - counts number of hard links to the file.
* User ID.
* Group ID.
* Device represented by this inode (if `inode` represents a device).
* File size (in bytes).
* Preferred block size for I/O.
* Number of blocks allocated to the file.
* Last access timestamp.
* File creation timestamp.
* Last modification timestamp.
* Last status change timestamp.