Thanks **The Morris Worm** - first web worm that used buffer overflow exploit.

It occurs when the data volume exceeds the capacity of a memory buffer. In this way extra data can be written (or red) to the memory space right after buffer's, and this behavior we need to prevent.
### Stack-based overflow:
As an example, nowadays, many languages use [[Stack frame]] technology (so we know where frame pointers and return addresses and etc are stored), so with use of buffer overflow exploit we can change return address to what we want and run arbitrary commands at this address... Or, that sounds not so scary, we can just read or change data, that was allocated on stack.

Trampoline technique: Instead of setting the return address directly to the address of the stack, they set the return address to an instruction that in turn passes execution to the stack.

How to beat NX? The `system()` function, being part of a system [[Library]], is already executable. The exploit doesn't have to execute code from the stack, it just has to read the command line from the stack. This technique is called "return-to-libc"  (`libc` is the name of the Unix [[Library]] that implements many key functions, including `system()`, and is typically found loaded into every single [[UNIX]] [[Process]], so it makes a good target for this kind of thing)
![[Pasted image 20231011175116.png]]
Another moment... Stack has a finite size, soo if the user input is longer than the stack space, the program cannot verify it and stack overflows. The overflow can become a security threat or loophole when combined with malicious inputs.
### Integer overflow attack
Mmm, just an integer overflow so we need more memory to store the value. Hello Python with floating int size (`int8`, `int16`, `int32`)
### Format strings overflow attack
Using string formatting [[Library]] functions, such as `printf` or `sprintf`, to write large strings to the buffer with less size or `gets`, `scanf`, and `strcpy` that have not been bounds-checked to read more information that we are allowed to.
### Unicode overflow attack
A Unicode overflow attack exploits the memory required to store a string in the Unicode format rather than the ASCII characters. Attackers use this type of buffer overflow attack when the program expects all inputs in ASCII characters.

## How to prevent:
* Address space layout randomization (**ASLR**): requires the attacker to know the location of an executable in memory. **ASLR** randomly arranges the address space positions of key data areas of a [[Process]], including the base of the executable and the positions of the stack, heap and libraries (check [[Virtual memory]]). 

	 Before **ASLR**, EXEs would always be loaded at an address of `0x0040000` and could safely make assumptions on that basis. After **ASLR**, that's no longer the case. For example, one restriction is the amount of randomness it can provide. This is especially acute on 32-bit systems. Although the memory space has more than 4 billion different addresses, not all of those addresses are available for loading libraries or placing the stack. Executables and libraries generally have to be loaded so that they start on, at the very least, a page boundary. Normally, this means they must be loaded at an address that's a multiple of 4,096.
	 
	 Platforms can have similar conventions for the stack; Linux, for example, starts the stack on a multiple of 16 bytes. Systems under memory stress sometimes have to further reduce the randomness in order to fit everything in. It means that we can guess the the stack address.
	 
	 But on 64-bit systems, there's so much address space that this kind of guessing approach is untenable. The attacker could be stuck with a one in a million or one in a billion chance of getting it right, and that's a small enough chance as to not matter.

* Data execution prevention: flagging areas of memory as executable or non-executable.

	**NX: No Xecute principle**
	 
	These systems strive to make memory either _writeable_ (suitable for buffers) or _executable_ (suitable for libraries and program code) but not _both_. Thus, even if an attacker can overflow a buffer and control the return address, the processor will ultimately refuse to execute the shellcode.
	
	Whichever name you use, this is an important technique not least because it comes at essentially no cost. This approach leverages protective measures built into the processor itself as part of the hardware support for [[Virtual memory]].
	
	The data structures used to store the mapping don't just include the location (physical memory, disk, nowhere) of each page; they also contain (usually) three bits defining the page's protection: whether the page is readable, whether it is writeable, and whether it is executable.

* Structured exception handling overwrite protection: block overriding SEH.

https://arstechnica.com/information-technology/2015/08/how-security-flaws-work-the-buffer-overflow/ - about stack overflow and prevention methods.
https://habr.com/ru/articles/463227/ - heap overflow task solved.