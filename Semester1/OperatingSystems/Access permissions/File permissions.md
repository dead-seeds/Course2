
Permissions mask has 12-bit. Greatest 3 bits are for `setuid`, `setgid` and sticky-bits. Next 9 bits are for access permissions. These bits can be set with 3 3-bit numbers (0-7).

The three digits of the `chmod` code set permissions for these groups in this order:
1. Owner (you)
2. Group (a group of other users that you set up)
3. World (anyone else browsing around on the file system)

Examples:

|   |   |
|---|---|
|chmod 700|Only you can read, write to, or execute file.|
|chmod 777|Everybody can read, write to, or execute file.|
|chmod 744|Only you can read, write to, or execute file. Everybody can read file.|
|chmod 444|You can only read file, as everyone else.|


What these numbers are:

| |                                                          |   |
|-|----------------------------------------------------------|---|
|**0**| No permission                                            |---|
|**1**| Execute permission                                       |--x|
|**2**| Write permission                                         |-w-|
|**3**| Execute and write permission: 1 (execute) + 2 (write) = 3|-wx|
|**4**| Read permission                                          |r--|
|**5**| Read and execute permission: 4 (read) + 1 (execute) = 5  |r-x|
|**6**| Read and write permission: 4 (read) + 2 (write) = 6      |rw-|
|**7**| All permissions: 4 (read) + 2 (write) + 1 (execute) = 7  |rwx|


