* OPEN_MAX
>"Soft" (administrative) limit can be set with `setrlimit(2)` with `RLIMIT_NOFILE` or `ulimit(1)`. "Hard" limit is set by the system [[Kernel]]. We can define "hard" limit with `sysconf(2)` call with parameter `_SC_OPEN_MAX`.
>
>In our Solaris, "hard" limit is set with parameter `rlim_fd_max` in the file ` /etc/system (system(4));`. To change it you need admin permissions and reboot.
