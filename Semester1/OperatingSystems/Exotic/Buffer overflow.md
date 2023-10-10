It occurs when the data volume exceeds the capacity of a memory buffer. In this way extra data can be written to the memory space right after buffer's, and this behavior we need to prevent. Nowadays, many languages use stack frame technology (so we know where frame pointers and return values and etc are stored), so with use of buffer overflow exploit we can access other frames or overwrite data. Also, in the same way we can perform tricks with heap and executable data.

Buffer overflow can be caused by library functions that have not been bounds-checked, which includes `gets`, `scanf`, and `strcpy`.

### Stack-based overflow:
A stack has a finite size, soo if the user input is longer than the stack space, the program cannot verify it and stack overflows. The overflow can become a security threat or loophole when combined with malicious inputs.
### Integer overflow attack
Mmm, just an integer overflow so we need more memory to store the value. Maybe in some languages it's a problem.
### Format strings overflow attack
Using string formatting library functions, such as `printf` or `sprintf`, to write large strings to the buffer with less size.
### Unicode overflow attack
A Unicode overflow attack exploits the memory required to store a string in the Unicode format rather than the ASCII characters. Attackers use this type of buffer overflow attack when the program expects all inputs in ASCII characters.

## How to prevent:
* Address space layout randomization (*ASLR*): requires the attacker to know the location of an executable in memory. *ASLR* randomly arranges the address space positions of key data areas of a [[Process]], including the base of the executable and the positions of the stack, heap and libraries (check [[Virtual memory]]).
* Data execution prevention: flagging areas of memory as executable or non-executable.
* Structured exception handling overwrite protection: block overriding SEH.