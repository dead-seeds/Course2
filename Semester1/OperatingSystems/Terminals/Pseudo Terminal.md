There are [[Terminal]]s already which solve the problem of abstracting the hardware. Why do 
we need _pseudo_ terminals (or pty for short) then?
## What problem do they solve?
Imagine, you want to write a terminal emulator: program that displays characters that programs output and redirect keyboard input into currently running ones. Suppose, you can read keyboard input from a terminal. How would you run a program that interacts with a terminal **and** display their output? Think of [[Shells]]

You can't give that program your terminal because you couldn't read what the program was writing to it. Hence couldn't display it on screen.

So you need to _trick_ a program into thinking that you gave it a terminal - give it a pseudo terminal.
## What are they?
Pseudo terminals are a pair of [[file]]s with special meaning for it's users and for [[Kernel]]
A process can create a pseudo terminal, becoming its **master**. This creates a new [[File descriptor]] associated with the pty. Each pseudo terminal has an associated **slave** end - a file which descriptor can be retrieved using a master descriptor, typically it lies in `/dev/pty/N` .
From now on, everything that is written to slave will be passed to master (through line discipline that is) and everything written to master - to slave. In that arrangement, master has to somehow emulate a behavior of a terminal. 
Ptys are treated just as terminals would in that they can be associated with a session. 
## Real-world examples
There are a number of uses in the real world and chances are, you already used a program that utilize them. 
### Terminal emulation
The problem this note started. Pseudo terminals allow terminal emulators (modern terminals basically) to be the middleman between [[process]]es in a [[session]] and windowing system (user).
### Remote access
With pseudo terminals problem with remotely accessing another computer becomes almost trivial. `ssh` can just go and talk to another ssh through [[socket]]s
### Multiplexing terminal
Canonical example here is `screen` but let's look at `tmux`. Tmux server is becoming a master for _multiple_ pseudo terminals, launching multiple sessions each with its own shell. Then, tmux client can connect to the server and choose what session they want to direct their output to. (Multiplexing terminal input).
### Scheme
Here is a scheme that shows how pseudo terminals can be used:
![[pseudo_terminals_scheme.jpg]]
## Further read
http://www.linusakesson.net/programming/tty/ - must read. Goes over historical context with terminals before diving into ptys.
Advanced programming in UNIX environment, chapter 19. Great book, recommended by [[Irtegov]]. Can be a little dense with examples. 