Compiling the program generates not only executable file, but also _constructors_ (initialization routines) and _destructors_ (termination routines). The linker must build two lists of these functions - a list of initialization functions, called `__CTOR_LIST__`, and a list of termination functions, called `__DTOR_LIST__`.

The prologue of a function (`_init`) appears in the `.init` section of _program.o_. `.init` section will be executed at program startup.
![[Disassembly init section.png]]

And there is  `_fini` in the _.fini_ section, that will be executed at the termination of the program.
![[Disassembly fini section.png]]

SRC for deeper research: https://gcc.gnu.org/onlinedocs/gccint/Initialization.html