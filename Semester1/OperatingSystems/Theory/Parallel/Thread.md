A thing, for that we make an illusion of continuous run.

`struct Thread` contains:
* Program counter
* Stack pointer
* Pointer to the next thread descriptor
* Pointer to the end of a thread list (or thread queue) to place previous thread in the end and let its next thread be current
