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
+ Deadlock definition:
  + A collection of threads are all blocked
  + Each thread is waiting for a resource owned by one of the other threads.
  + Since all threads are blocked, none can release their resources.

### 4.1 Deadlock Problems
+ Systems usually have multiple locks
+ Threads often need to hold multiple locks at the same time
+ 
### 4.2 Necessary Conditions for Deadlock
+ There are 4 necessary conditions for deadlock occur:
  + 1. **Limited access**: Resources cannot be shared. there are a finite number of threads that can simultaneously use a resource. 
  + 2. **No preemption**: Once given, a resource cannot be taken away.
  + 3. **Multiple independent requests**: Threads don't ask for resources all at once (hold resources while waiting)
  + 4. **Circular waiting**: Circularity in the graph of requests and ownership.

<div style = "text-align:center">
<img src ="/Media/OS/deadlock_illustrate.png">
</div>

### 4.3 Cause and solution forDeadlock
+ Deadlock can occur over antythig that causes waiting:
  + Locks
  + Network messages
  + Disk drive
  + Memory space exhausted/
+ Deadlock can occur over discrete resources(e.g locks) or quantities of a more continous resoucrce(pages of memory)
+ In general, don't know in advance which resources a thread will need.

+ *Solution*:
  + 1. Deadlock detection:
    + Determine when system is deadlocked.
    + Break the deadlock by terminating one of the threads.
    + Usually not practical in operating systems, but often used in database system where transactions can be aboarted and retried.
  + 2. Deadlock prevention: Eliminate one of the necessary conditions for deadlock.
    + Don't allow exclusive access $\to$ Not reasonable for most applications
    + Create enough resources so that they never run out $\to$ May work for things like disk space, but locks for synchronization are intentionally limited in number.
    + Allow preemption $\to$ Works for some resources but not others (e.g Can't preempt a lock)
    + Require threads to request all resources at the same time; either get them all or wait for them all.
      + Tricky to implement: must wait for several things without locking any of them.
      + Inconvenient for thread: hard to predict needs in advance. May require thread to over-allocate just to be safe.
    + Prevent circularities: all threads request resources in the same order (e.g always lock 1 before 2) $\to$ ordering lock $\to$ Most common approach used in operating system.