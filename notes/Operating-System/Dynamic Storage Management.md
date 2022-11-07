# Dynamic Storage Management
+ There are 2 basic operations in dynamic storage management:
  + Allocate a block with a given number of bytes
  + Free a previously allocated block
+ Approaching methods:
  + Stack allocation (Hierarchical): restricted, but simple and efficient.
  + Heap allocation: more general, but more difficult to implement, less efficient
  
## Stack Allocation
+ It's a temporary memory allocation scheme where the data members are accessible only if the method() that contained them is currently running
+ It allocates or de-allocates the memory automatically as soon as the corresponding method completes its execution.
+ Data stored on Stack can only be access by onwer thread

## Heap Allocation

+ Heap allocation used when allocation and release are unpredictable. 
+ Allocation and de-allocation need to be done by the progammer manually. 
+ Each program ran, they allocated and de-allocated memory in heap $\to$ clear memory in heap create holes $\to$ fragmentation $\to$ inefficient use of memory 

<div style='text-align:center'>
<src img = '/Media/Stack_Heap_Allocation.png'>
</fig>

## Storage Reclamation
