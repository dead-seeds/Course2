Check critical sections in [[CRITS (23-24)]].

Ways to deal with critical sections:
* Using immutable data
* Harmonic interactions (sockets, pipes)
* Copy-modify-merge:
	* Merging manually (like in GitHub)
	* Transaction mechanics
* LockLess coding (kinda impossible)

Intel processors have `lock` prefix, that means monopoly control of a tire while processing a command. 
ARM processors has `ldrex`/`stlex`, that are kinda same.

[[Scheduler]] - a manager that switch running [[Thread]]s. It takes control from one [[Thread]] and let the other be running since the moment he took the control from it.