`<signal.h>`

Signal - the method to send messages to the [[Kernel]] and to other [[Process]]es. Signal to other [[Process]] can only be sent through the [[Kernel]]. Signals can be sent by the [[Kernel]] to the [[Process]] or the whole [[Process group]].

Ways to send signals:
* [[sigsend()]]
* [[kill()]]
* [[alarm()]]
* some kind of event (`ctrl+c` or dividing by zero)

Every [[Process]] has **signal mask**, that describes what signals are blocked to be received for this process. `SIGKILL` and `SIGSTOP` can't be blocked with mask.

Check some [[Basic signals]].
