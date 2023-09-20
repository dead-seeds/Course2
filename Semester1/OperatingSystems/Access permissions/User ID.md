Each user in a [[UNIX]] system has a unique ID. [[File permissions]] are given based on that. (And a [[Group ID]]). 
There are a number of different user ids associated with a [[process]].
1. Real UID - User ID of a user who started the process
2. Effective UID - User ID of a user that is used to check permissions. Real and effective user ID are typically the same, but in some cases you want to take someone else's identity (typically root). Real and effective are different to allow switching back only to your real id. (And in case you are root - to any).
3. Saved UID - typically used in case a privileged process needs to become unprivileged temporarily. While switching from privileged to unprivileged is possible - the opposite is not true. To fix that, before switching to another uid, process stores EUID in SUID.
