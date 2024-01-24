Because of existence of [[Memory Management Unit]] between virtual memory address and physical one, [[OS]] can map files onto [[Virtual memory]]. This way, contents of file will be written to the page corresponding to mapped virtual segment.

Files might me mapped in different mode, some of them tell [[OS]] to save changed pages back to files on close. Close happens when [[OS]] takes page away, or it gets unmapped (It happens automatically on [[Process]] end of life). For specifics on this see `map 2 mmap`.
