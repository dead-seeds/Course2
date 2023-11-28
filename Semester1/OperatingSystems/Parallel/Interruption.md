When processor gets the signal at the input of IRQ, it perform the interruption.
What exactly does that mean:
* Saving PC, registers in the stack (check [[CRITS]] for the def of process context)
* Getting the _interruption handler_ address from the **interrupt vector table**
* Running the handler
* Restoring PC, register and the whole process context

The time from the moment interruption signal has been sent till the first command of the handler is **interrupt latency**.