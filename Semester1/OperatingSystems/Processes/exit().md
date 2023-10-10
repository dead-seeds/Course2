`void exit(int status)`

Exit the [[Process]] with some sTaTuS...

`status` can be got with `wait(&status)`. BUT status we'll get will not be exactly `int` we sent with `exit`, we need to `WEXITSTATUS(status)`. 