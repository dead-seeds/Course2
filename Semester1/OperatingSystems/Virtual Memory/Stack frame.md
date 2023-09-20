Each function (including main) creates a stack frame. It contains following:
1. Pointer to return from the function
2. Function arguments (if they did not fit in registers)
3. Local non-static variables
4. In C++ there could be exception handlers and local variables destructors