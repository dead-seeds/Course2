Every thread has its own stack, pointer to that stack is stored in thread descriptor.

When ThreadSwitch changes active thread:
* Restores PC of the next thread run
* Saves actual SP in thread descriptor
* Restores SP from the next thread's descriptor
* Running of a new thread continues from the position we stopped the previous run, because its address was stored in Stack