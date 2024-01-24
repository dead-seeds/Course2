*read `man signal-safety` about async-signal-safe functions.* There you can read about reasons why all `stdio` functions are not safe.

Signal handler **must** have _mutual exclusion_ property. Every shared data modification must be a **transaction**.

In fact, the [[Signal]] can be sent to our thread at every moment (it means, not only when our thread is running, because of the illusion of parallelism), so we should use only thread-safe functions in it.