This is a struct containing information about a [[Signal]] that was (will be) sent (received). Here are the most important bits. For more information see `man sigaction`.
- Signal number. Number that represents the type of signal. For example: SIGCHLD, SIGSEGV, SIGKILL. For specifics see `man 7 signal`. (Put -s on solaris)
- Signal code. Number that represents _why_ signal was sent. Interpretation of this number is different depending on the signal number. For specifics see `man sigaction`
- [[PID]] of a sending [[Process]]
- Real [[User ID]] of sending [[Process]] 