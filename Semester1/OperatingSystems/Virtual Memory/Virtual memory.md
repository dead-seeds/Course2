Virtual memory is a concept that enables process sandboxing by creating a table that maps from virtual address to the real one. #doublecheck This way [[Kernel]] can have fine-grained control over which resources can be access from a particular process.
In [[UNIX]] there are block of shared memory included in multiple processes' virtual memory mapping.