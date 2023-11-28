`void exit(int status)`

`status` can be got with `wait(&status)`. BUT status we'll get will not be exactly `int` we sent with `exit`, we need to `WEXITSTATUS(status)`. 