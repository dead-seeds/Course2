[[Process group]] - a collection of processes, typically involved in doing one [[task]]. Each process group is assigned with a [[PGID]]. Process group can have a leader. [[PID]] of a group leader is equal to [[PGID]] of it's group.
Termination of process group leader does not close the group - it will exist until there is no processes left in it. Timeframe from group creation to last process leaving is called group's lifetime.
#syscall `pid_t getpgrp(void);` returns caller's [[PGID]].
#syscall #canfail`pid_t getpgid(pid_t pid);` returns [[PGID]] of a process with given [[PID]].
#syscall #canfail `int setpgid(pid_t pid, pid_t pgid);` sets [[PGID]] of a process with [[PID]] = pid to pgid.  0 passed is interpreted as a caller's [[PID]] (both arguments)