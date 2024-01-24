### Race condition
A condition when the order of execution of parallel [[Process]]es determines the result of the program. Well, order matters all the time but with race condition result is not consistent over time: it can be different from time to time.
### Dead lock
If multiple locks are nested in a different order, dead lock can appear when process1 locks `lock1` while process2 locks `lock2`. After that point, process1 will never be able to lock `lock2` since it's already lock and process2 won't lock `lock1`. Neither could continue...
```
lock(lock1) {
	lock(lock2) {
		// stuff
	}
}
```
```
lock(lock2) {
	lock(lock1) {
		// stuff
	}
}
```