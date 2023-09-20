There are a number of system variables:
- Max path length
- ... #todo

In the past, all of them were declared in a header files. Which meant that any time they are changed, all programs would have to be recompiled. To mitigate that issue, those variables were moved to (a conf file? #ask) runtime. That way, programs no longer need to recompile on system variable change.
```
long sysconf(int name);
long fpathconf(int fildes, int name);
long pathconf(const char *path, int name);
```
`pathconf` here gives information about a file at path