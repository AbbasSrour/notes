## Address Space
Address spaces is the set of accessible addresses and the state associated with them. For a 32-bit processor there is an upper limit of 4 billion addresses while a 65-bit processor has 18 quadrillion addresses. 

### Segments
A segment is a hardware register that has the base and bound coded in that segment.

### Paged Virtual Address Space
Breaks the entire virtual address space into equal size chunks (pages) with a base for each, being all of the same size it makes it easy to place each page in memory and translate address using a page table.