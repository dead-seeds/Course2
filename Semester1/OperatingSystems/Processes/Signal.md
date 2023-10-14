`<signal.h>`

Signal - a method of asynchronous communication between [[Kernel]] and [[Process]]es. Signal to other [[Process]] can only be sent through the [[Kernel]]. Signals can be sent by the [[Kernel]] to the [[Process]] or the whole [[Process group]].

When [[Process]] receives a signal, it performs a default action (which is different depending on the signal) or, if default was overwritten by a previous call to [[sigaction]], calls a specific handler 

Each sent signal has an associated struct [[siginfo_t]] which contain a lot of information: what is the signal, why it was sent, who sent it, [[errno]], when it was consumed and etc.

Ways to send signals:
* [[sigsend()]]
* [[kill()]]
* [[alarm()]]
* some kind of event (`ctrl+c` or dividing by zero)

Every [[Process]] has **signal mask**, that describes what signals are blocked to be received for this process. `SIGKILL` and `SIGSTOP` can't be blocked with mask.

Check some [[Basic signals]].
