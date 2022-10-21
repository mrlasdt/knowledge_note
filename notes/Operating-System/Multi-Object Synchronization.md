# Multi-Object Synchronization

## 1. Lock Design Patterns

+ There are 4 well-known design patterns to increase concurrency:
  + **Fine-Grainded Locking**: partition an object's state into different subsets each protected by a different lock. 
  + **Per-Processor Data Structures**: Partition an object's state so that all or most accesses are performed by threads running on the same processor. 
  + **Ownership Design Pattern**: Remove a shared object from a shared container so that only a single thread can read or modify the object. 
  + **Stages Architecture**: Divide system into multiple stages, so that only those threads within each stage can access that stage's shared data. 
## 2. Lock Contention

1. **MCS Locks**: MCS is an implementation of a spinlock optimized for the case when there are a significant number of waiting threads.
   + The normal lock work fine, but it got 2 main **problems**: 
     + communicated between threads is too much $\to$ overhead time is big.
     + Can't guarantee FIFO ordering amongst the processors competing for the lock.
   + MCS Lock mechanism:
     + Use a queue to arrange Lock acquired 
     + Use a ticket(flag) to enable thread access to lock
2. **RCU locks**: RCU is an implementation of a reader/writer lock, optimized for case when there are many more readers and writers by reducing overhead for readers at a cost of increased overhead for writers.
  
## 3. Multi-Object Atomicity

## 4. Deadlock

+ *A deadlock is a cycle of waiting among a set of threads, where each thread waits for some other thread in the cycle to take some action*
+ 