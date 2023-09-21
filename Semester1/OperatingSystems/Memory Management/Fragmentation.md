## Internal
Occurs if requested amount of bytes is smaller than block size. (Instead of allocating whole free block we split it, so now one block is allocated and another is free. Our list of free blocks updates.)

## External
Occurs when there is enough heap memory but no single block is large enough for allocation. (There can be a situation when there are two empty blocks one after another and if we allocate them both, we'll success. So to avoid that problem we delete pointer to the second block from list of free blocks and now we have logically correct list. In other words, we coalesce two free blocks into one.)