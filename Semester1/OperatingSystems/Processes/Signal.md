`<signal.h>`

Signal - a method of asynchronous communication between [[Kernel]] and [[Process]]es. Signal to other [[Process]] can only be sent through the [[Kernel]]. Signals can be sent by the [[Kernel]] to the [[Process]] or the whole [[Process group]].

When [[Process]] receives a signal, it performs a default action (which is different depending on the signal) or, if default was overwritten by a previous call to [[sigaction]] (or `signal()`), calls a specific [[Signal handler]].

Let's look closely at `signal()`:
* After receiving the signal and calling a handler, signal disposition is set to default.
* `signal()` returns address of the previous signal disposition (or `SIG_DFL` or `SIG_IGN`).

Now let's check `int sigaction (int sig, const struct sigaction *act, struct sigaction *oact)`:
* Structure [[sigaction]] has  `void \*sa_handler` (for `sig` signal), `void \*sa_sigaction (int, siginfo_t \*, void \*)`, `sigset_t sa_mask` and `int sa_flags`. Sa_handler is responsible for actions we'll do when the signal `sig` will be received.
* If `sa_handler` is not `NULL` and we received the signal `sig`, `sa_mask` bits are changed according to signals we want to block while signal handling. Only after signal handler finishes its actions, `sa_mask` is set to default. That helps us to deal with multiple signals at a time, because UNIX doesn't support signal queues.
* After handling the signal we don't need to change signal disposition to our custom.


Each sent signal has an associated struct [[siginfo_t]] which contain a lot of information: what is the signal, why it was sent, who sent it, [[errno]], when it was consumed and etc.

Ways to send signals:
* [[sigsend()]]
* [[kill()]]
* [[alarm()]]
* some kind of event (`ctrl+c` or dividing by zero)

Every [[Process]] has **signal mask**, that describes what signals are blocked to be received for this process. `SIGKILL` and `SIGSTOP` can't be blocked with mask.

Check some [[Basic signals]].
