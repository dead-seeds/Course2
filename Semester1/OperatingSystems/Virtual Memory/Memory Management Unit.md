MMU can implement various strategies.
## Base addressing
Each process occupies a contiguous memory location.
Process pointer -> MMU -> Process pointer + base -> Real memory.
There also an upper limit on process pointer.
|<--OS-->|<--Process 1-->|<--Free-->|<--Process 2-->|
Problems:
1. External fragmentation
2. Increasing memory for a process can involve moving another process's base
## Multiple-base addressing
Same as base addressing, but each process can have multiple base-limits. Different platforms have different base counts. For example, [[PDP-11]] has 8 of those
Process pointer -> MMU -> Base\[selector] + shift -> Real memory
When 8 is not enough, MMU starts keeping track of a table with all memory chunks: base, limit, flags (write, execute)
## Page based addressing
Multiple-base addressing with a lot of chunks with all of them the same size is called page based addressing. 

[[Translation Lookaside Buffers]]
