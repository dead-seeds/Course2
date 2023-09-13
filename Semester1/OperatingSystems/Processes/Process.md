Process - an program executing in a sandbox with restricted privileges. Each process has [[Virtual memory]] mapped to it that dictates which memory can be accessed. Attempt to access memory out of range leads to process being killed by a [[Kernel]] passing a [[signal]]. It can be intercepted.
Being placed in a sandbox in [[User mode]] the only way out to the real world is [[System call]]s.
[[UNIX]] assigns each process a unique positive integer - process ID, [[PID]]. They are unique at each moment but not overall - [[Kernel]] reuses them over time. 
#syscall `pid_t getpid()` returns [[PID]] of current process

Every process except [[init]] has a parent from which it was [[fork]]ed. In [[Solaris]] init has a parent pseudo process sched with pid = 0. (It does not have virtual memory tho).
Every process has a [[Process group]] and a [[Terminal Session]] containing it. A [[deamon]] is a process which [[Terminal Session]] does not have a [[Terminal]].

Processes can't communicate with each other directly - all the talking must go through [[Kernel]] using [[ipc]] channels. That way we can place processes in [[container]]s, attach different privileges and etc. Sandbox, basically

Process structures:
- TEXT - machine code
- DATA - initialized static data
- BSS - not initialized static data
- STACK
- Heap
- Dynamic segments #ask
- User area process descriptor in kernel - legacy because now kernels have multiple threads and its no longer possible to map this to one area. (Its NOT user memory)
	- Stack of process in kernel
	- Open file descriptors
	- Process attributes

Because all processes are isolated from hardware, killing one process won't affect others.