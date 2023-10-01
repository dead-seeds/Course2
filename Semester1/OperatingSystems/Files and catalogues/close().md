`close(int fd)`

OMG, `close` closes the [[File descriptor]] (it no longer refers to any file description) and it can be reused. [[File permissions]], that process had, removes. If this is the last `fd` of connected file description, resources are freed.

`close()` returns 0 on success and -1 on error ([[errno]] is set to indicate the error).
