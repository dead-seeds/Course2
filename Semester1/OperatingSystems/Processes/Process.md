Process - an program executing in a sandbox with restricted privileges. Each process has [[Virtual memory]] mapped to it that dictates which memory can be accessed. Attempt to access memory out of range leads to process being killed by a [[Kernel]] passing a [[signal]]. It can be intercepted.

Being placed in a sandbox in [[User mode]] the only way out to the real world is [[System call]]s.
[[UNIX]] assigns each process a unique positive integer - process ID, [[PID]]. They are unique at each moment but not overall - [[Kernel]] reuses them over time. 
#syscall `pid_t getpid()` returns [[PID]] of current process

Every process except [[init]] has a parent from which it was [[fork]]ed. In [[Solaris]] `init` has a parent pseudo process `sched` with pid = 0. (It does not have virtual memory tho).

Every process has a [[Process group]] and a [[Terminal Session]] containing it. A [[deamon]] is a process which [[Terminal Session]] does not have a [[Terminal]].

Processes can't communicate with each other directly - all the talking must go through [[Kernel]] using [[ipc]] channels. That way we can place processes in [[container]]s, attach different privileges and etc. Sandbox, basically

Because all processes are isolated from hardware, killing one process won't affect others.

Attributes (other than [[Virtual memory]]):
Kernel:
1. Process
	1. PID
	2. Parent ID
	3. [[Process group]] ID
	4. [[Terminal]]
	5. [[Session]] (terminal)
	6. limits
2. User
	1. UID (real + effective + saved )
	2. GID (real + effective)
3. File system
	1. Open files
	2. Current Working Directory
	3. [[Limits]] (umask, ulimit)
	4. Root directory
Userspace:
1. Command line arguments
2. Environment variables