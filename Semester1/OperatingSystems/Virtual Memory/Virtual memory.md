Virtual memory is a concept that enables process sandboxing by creating a table that maps from virtual address to the real one. #doublecheck This way [[Kernel]] can have fine-grained control over which resources can be access from a particular process.
In [[UNIX]] there are block of shared memory included in multiple processes' virtual memory mapping.


[Source of virtual memory layout](https://github.com/illumos/illumos-gate/blob/master/usr/src/uts/i86pc/os/startup.c)
32-bit Kernel's Virtual memory layout:

|              |                        |                                 |
|--------------|------------------------|---------------------------------|
|0xFFC00000 ---|------------------------|------------------------ ARGSBASE| 
|0xFF800000 ---|------------------------|-------------------- SEGDEBUGBASE|
|		       |:      	                |                                 |
|              |      Kernel Data       |                                 |
|              |:                       |                                 |
|              |:                       |                                 |
|0xFEC00000 ---|------------------------|---------------------------------|
|              |:      	                |                                 |
|              |      Kernel Text       |                                 |
|              |:                       |                                 |
|              |:                       |                                 |
|0xFFC00000 ---|------------------------|------------------------ ARGSBASE|
|		       |: 	    	            |                                 |
|              |        debugger        |                                 |
|              |:                       |                                 |
|              |:                       |                                 |
|0xFF800000 ---|------------------------|-------------------- SEGDEBUGBASE|
|		       |:          	            |                                 |
|              |       Kernel Data      |                                 |
|              |:                       |                                 |
|              |:                       |                                 |
|0xFEC00000 ---|------------------------|---------------------------------|
|              |      Kernel Text	    |                                 |
|0xFE800000 ---|------------------------|- KERNEL_TEXT (0xFB400000 on Xen)|
|		       |          GDT           |--------------- GDT page (GDT_VA)|
|		       |       debug info       |------ debug info (DEBUG_INFO_VA)|
|		       |:           			|                                 |
|		       |   page_t structures	|                                 |
|		       |   memsegs, memlists,	|                                 |
|		       |   page hash, etc.	    |                                 |
|--------------|------------------------|ekernelheap,valloc_base(floating)|
|		       |:		            	|                                 |
|		       |:                       |                                 |
|		       |	     kvseg	        |(segkp,just an arena in the heap)|
|		       |:                       |                                 |
|		       |:                       |                                 |
|--------------|------------------------|- kernelheap (floating)          |
|		       |        Segkmap	        |                                 |
| 0xC3002000  -|------------------------|- segmap_start (floating)        |
|		       |	    Red Zone	    |                                 |
| 0xC3000000  -|------------------------|- kernelbase/userlimit (floating)|
|		       |:                       |                                 |
|		       |     Shared objects	    |                                 |
|		       |:                       |                                 |
|		       |:                       |                                 |
|		       |	   user data	    |                                 |
|--------------|------------------------|                                 |
|		       |	   user text	    |                                 |
| 0x08048000  -|------------------------|                                 |
|		       |	   user stack	    |                                 |
|		       |:                       |                                 |
|		       |	    invalid		    |                                 |
| 0x00000000---|------------------------|---------------------------------|


64-bit Kernel's Virtual memory layout. (assuming 64 bit app):

|                      |                       |                               |
|----------------------|-----------------------|-------------------------------|
| 0xFFFFFFFF.FFC00000  |-----------------------|- ARGSBASE                     |
|			           |:                      |                               |
|			           |	  debugger (?)	   |                               |
|			           |:                      |                               |
| 0xFFFFFFFF.FF800000  |-----------------------|- SEGDEBUGBASE                 |
|			           |         unused		   |                               |
|			           |+                      |                               |
|			           |      Kernel Data	   |                               |
| 0xFFFFFFFF.FBC00000  |-----------------------|                               |
|			           |      Kernel Text	   |                               |
| 0xFFFFFFFF.FB800000  |-----------------------|- KERNEL_TEXT                  |
|			           |:                      |                               |
|			           |---    debug info   ---|- debug info (DEBUG_INFO_VA)   |
|			           |---       GDT       ---|- GDT page (GDT_VA)            |
|			           |---       IDT       ---|- IDT page (IDT_VA)            |
|			           |---       LDT       ---|- LDT pages (LDT_VA)           |
|			           |+			           |                               |
|			           |       Core heap       | (used for loadable modules)   |
| 0xFFFFFFFF.C0000000  |-----------------------|- core_base / ekernelheap      |
|			           |	    Kernel		   |                               |
|			           |+                      |                               |
|			           |	     heap		   |                               |
| 0xFFFFFXXX.XXX00000  |-----------------------|- kernelheap (floating)        |
|			           |	     segmap		   |                               |
| 0xFFFFFXXX.XXX00000  |-----------------------|- segmap_start (floating)      |
|			           |    device mappings	   |                               |
| 0xFFFFFXXX.XXX00000  |-----------------------|- toxic_addr (floating)        |
|			           |	     segzio		   |                               |
| 0xFFFFFXXX.XXX00000  |-----------------------|- segzio_base (floating)       |
|			           |        segkvmm	       |                               |
|			           |:			           |                               |
|			           |:			           |                               |
|			           |:			           |                               |
| 0xFFFFFXXX.XXX00000  |-----------------------|- segkvmm_base (floating)      |
|			           |	     segkp		   |                               |
|			           |-----------------------|- segkp_base (floating)        |
|			           |   page_t structures   |  valloc_base + valloc_sz      |
|			           |   memsegs, memlists,  |                               |
|			           |   page hash, etc.	   |                               |
| 0xFFFFFE00.00000000  |------------------------|-valloc_base (lower if >256GB)|
|			           |	     segkpm		    |                              |
|			           |:			            |                              |
| 0xFFFFFD00.00000000  |------------------------|-SEGKPM_BASE (lower if >256GB)|
|			           |	    Red Zone	    |                              |
| 0xFFFFFC80.00000000  |------------------------|-KERNELBASE (lower if >256GB) |
| 0xFFFFFC7F.FFE00000  |------------------------|-USERLIMIT (lower if >256GB)  |
|			           |       User stack	    |-User space memory            |
|			           |:			            |                              |
|			           |   shared objects, etc	|	(grows downwards)          |
|			           |:                       |                               |
|			           |:			            |                               |
|			           |:                       |                               |
| 0xFFFF8000.00000000  |------------------------|                               |
|			           |:                       |                               |
|			           |:                       |                               |
|			           |:         			    |                               |
|			           |    VA Hole / unused	|                               |
|			           |:			            |                               |
|			           |:                       |                               |
|			           |:                       |                               |
| 0x00008000.00000000  |------------------------|                               |
|			           |:			            |                               |
|			           |:			            |                               |
|			           |:                       |                               |
|			           |	   user heap	    |	(grows upwards)             |
|			           |:			            |                               |
|			           |	   user data	    |                               |
|			           |------------------------|                               |
|			           |	   user text	    |                               |
| 0x00000000.04000000  |------------------------|                               |
|			           |        invalid		    |                               |
| 0x00000000.00000000  |+----------------------+|                               |

**Kernel context** - part of a kernel memory needed to make syscalls
**Red Zone** - zone to catch kernel memory address bugs
**Shared objects** - shared libraries, grows downwards
**User heap** - heap (malloc uses it), grows upwards
**User stack** - position of this 
**Invalid** - zone of invalid addressed. Made to catch a bunch of mistakes with memory addresses. Typically objects are just small nums