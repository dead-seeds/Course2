---
tags:
  - syscall
---
System calls is a function that calls [[Kernel]] code. They each have a wrapper that looks like just a function call.
Syscalls can check your authorization and privileges: for file access, etc.
They are expensive to call because changing from [[User mode]] to [[System mode]] requires additional movements. That's why standard library function try hard to save on syscalls. It's probably a good idea to use std function for that reason. 
> All [[man]] pages for syscalls available on [[Solaris]] can be accessed  [here](https://illumos.org/man/2/all). Or
> `man %name_of_syscall% 2` in your [[Linux]] terminal.

>Source code of all systems calls in [[Linux]] (NOT [[UNIX]]) can be found in the [repo](https://github.com/torvalds/linux/). Do not search by functions, but by plain text bc syscalls are defined like this: `SYSCALL_DEFINEX(name, ...)` where X is a number of arguments in `...`. And [[GitHub]] does not see them as functions. Weird stuff. C, you know.