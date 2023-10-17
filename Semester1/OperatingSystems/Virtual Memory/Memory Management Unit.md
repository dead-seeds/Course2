MMU is a hardware solution for mapping virtual memory into different physical memory. It is placed on the address bus. It can implement various strategies for doing it's job.
There are instances, where virtual address size does not equal physical address size.
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
Multiple-base addressing with a lot of chunks with all of them the same size is called page based addressing. With page based addressing a translation table exists in RAM (it's pretty big) which contains information about each page:
- Flags 
	- Dirty
	- Used
	- Supervisor bit
	- Existence bit (see Multilevel translation)
	- and others
- Permissions (Read, Write, Execute)
- Physical address
### Translation Lookaside Buffers 
Because memory access into RAM is very slow, MMU has a cache of most used pages. It is separate from processor data/instruction cache. TLB does not help if a program uses addresses from a lot of different pages.

In [[ARM]] processors (in contrast to [[Intel]]) TLB has addresses with ASI identifier, so we can switch [[Process]] without TLB cache reset. [[Intel]] cannot add this kind of feature, because they'll break back compatibility with old [[OS]]es.
If a page is not mapped to physical memory, an Page fault exception is thrown.
### Page swapping
[[OS]] catches Page fault exception and looks for memory to map to given page. It may need to take away page from another (or same) process. Of course, [[OS]] tries to take the least important page using heuristics. One way to do it is clock method. 
This is possible because [[OS]] has access to translation table. 
### Multilevel translation
Even one full table of [[virtual memory]] mapping is very big, each selector + base is divided into three parts. Each of them has a mapping table. If a one of three page lookups has existence bit not marked, then it stops with exception. This allows to not maps a bunch of pages on the lower level hence memory savings.  