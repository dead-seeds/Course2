There has to be ways to dynamically allocate memory. There are a number of techniques to do that:
<<<<<<< HEAD
- [[Stack allocator]]s
- Double
- [[Fixed-sized blocks allocator]]s
- [[Slab allocator]]s
## Allocation strategies
- Best fit
- First fit
- Worst fit

## Garbage collection
- Designed to fix memory leaks
There are several strategies to collect the garbage:
1. Reference counting. Each memory location (object) has a field - number of alive links. When the last reference to a memory location dies (# of links == 0), memory is collected. Examples: [[Basic]], [[COM]], [[Lotus Software Extension]]
	1. Does not allow cyclic lists
2. Mark and sweep. Recursively going through by links all alive objects and marking alive objects. Examples: [[Java]], [[Emacs List]].
	1. Environment has to be stopped completely (all threads even). This is expensive. To the point of taking 50% of the execution time. (That was in the old times)
	2. There are different strategies that do not involve blocking the whole world, but they have their own problems.
	3. Alive objects are marked. (Starting from stack, local variables)
	4. Objects have non-deterministic lifetimes. That is bad for certain resources: files, sockets, etc. Because they live arbitrarily long (which is bad)
3. Copying garbage collection. Similar to mark and sweep, but instead of freeing garbage it *copies* non-garbage to another part of the memory (a half, typically). Another benefit is heap defragmentation.
4. Generational garbage collection. Divides memory into even more chunks (For different generations) in hope of reduce overhead of allocating small objects.
Almost all garbage collection strategies are targeted at reducing stop-world time while moving a lot of work into background threads.
=======
- Stack
- Pool, heap - a list of free blocks

## Allocation strategies
- Best fit
- First fit
- Worst fit
>>>>>>> be7dfd4 (Start of dynamic memory management, good + bad source to find information, file clarifications)
