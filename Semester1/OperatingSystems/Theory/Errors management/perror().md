`perror(const char *s)`

The `perror()` function produces a message on standard error output. Firstly it prints `s` with a colon and a blank after, then error message corresponding to the current value of [[errno]]. The function `perror()` serves to translate this error code into human-readable  form.

Note that [[errno]] is undefined after a successful [[System call]] or [[Library]] function call: this call may well change this variable, even though it succeeds, for example because it internally used some other library function that failed.
