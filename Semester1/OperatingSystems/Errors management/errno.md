`#include <errno.h>`

This is an integer variable, which is set by [[System call]]s and [[Library]] functions in the event of an error. 

The value of `errno` is never set to zero by any [[System call]] or [[Library]] function.
**BUT**
For some system calls `-1` is a valid return on success. In such cases, `errno` can be set to zero before the call, and then can be checked to be a nonzero value.
The `errno(1)` command can also be used to look up individual error numbers and names.

**!!!`errno` is thread-local, setting it in one thread doesn't affect its value in any others!!!**