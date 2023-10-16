Thanks **The Morris Worm** - first web worm that used buffer overflow exploit.

It occurs when the data volume exceeds the capacity of a memory buffer. In this way extra data can be written (or red) to the memory space right after buffer's, and this behavior we need to prevent.

### Stack-based overflow:
https://web.ecs.syr.edu/~wedu/seed/Book/book_sample_buffer.pdf - huge pdf about stack-based buffer overflow
https://arstechnica.com/information-technology/2015/08/how-security-flaws-work-the-buffer-overflow/ - about stack overflow and prevention methods.

As an example, nowadays, many languages use [[Stack frame]] technology (so we know where frame pointers and return addresses and etc are stored), so with use of buffer overflow exploit we can change return address to what we want and run arbitrary commands at this address... Or, that sounds not so scary, we can just read or change data, that was allocated on stack.

Trampoline technique: Instead of setting the return address directly to the address of the stack, they set the return address to an instruction that in turn passes execution to the stack.

How to beat NX? The `system()` function, being part of a system [[Library]], is already executable. The exploit doesn't have to execute code from the stack, it just has to read the command line from the stack. This technique is called "return-to-libc"  (`libc` is the name of the Unix [[Library]] that implements many key functions, including `system()`, and is typically found loaded into every single [[UNIX]] [[Process]], so it makes a good target for this kind of thing)
![[Pasted image 20231011175116.png]]
Another moment... Stack has a finite size, soo if the user input is longer than the stack space, the program cannot verify it and stack overflows. The overflow can become a security threat or loophole when combined with malicious inputs.

### Heap-based overflow

https://github.com/shellphish/how2heap - repo with many types of heap exploitation techniques.
https://habr.com/ru/articles/463227/ - heap overflow task solved. (but not very good explanation)

You cannot overwrite the return address of `main` like you could with a stack based buffer overflow. Like information on the stack, though, the compiler might put things in places that you might not expect.

* Overwriting Function Pointers:
http://hamsa.cs.northwestern.edu/readings/heap-overflows/

By overflowing a buffer and overwriting the function pointers stored on the heap, an attacker can change the flow of execution and cause the application to call malicious code with elevated privileges.

* [[free()]] exploit (glibc 2.3.3+ has corrupted double-linked list check...):
https://www.win.tue.nl/~aeb/linux/hh/hh-11.html#ss11.2
https://www.opennet.ru/base/sec/heap_overflow.txt.html - Opennet is cringe, but this old paper is very good for understanding.

By overflowing a buffer and overwriting the metadata associated with an object stored on the heap, you might be able to overwrite the memory table pointer so that when `free()` runs, it frees up something other than what it originally allocated. When overwriting the size field, we must be careful that the computed location of the next chunk lies in allocated memory, not to cause a segfault in [[free()]]. 

The C program does not call `free()` directly, since the address is unknown at translation time. The call is indirect via an entry in the program linking table that is filled by the dynamic loader (`.plt` segment in `objdump -d progr_obj`). If we overwrite that entry with our favorite address, we will jump there instead. So we can place some stack address in one of them to crash the program. If we place some correct address of our script on the heap in there, we'll jump into it.

* UAF (Use After Free exploit):
https://ctf101.org/binary-exploitation/heap-exploitation/


### Integer overflow attack
Mmm, just an integer overflow so we need more memory to store the value. Hello Python with floating int size (`int8`, `int16`, `int32`)
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
