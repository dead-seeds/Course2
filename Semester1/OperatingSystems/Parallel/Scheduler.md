When `ThreadSwitch` changes active [[Thread]]:
* Restores PC of the next thread run
* Saves actual SP in thread descriptor
* Restores SP from the next thread's descriptor
* Running of a new thread continues from the position we stopped at the previous run, because its address was stored in the Stack