A primitive is an abstract object with not-defined type (bytes basically) with some actions defined on it. You should always use those through the methods defined. Otherwise state is not guaranteed.
In the case of synchronization primitives, that means bypassing their official interface can cause [[Problems]].
* [[Spinlock]]
* [[Pipe]]
* [[Mutex]]
* [[Semaphore]]