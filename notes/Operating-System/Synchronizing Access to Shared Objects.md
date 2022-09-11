# Synchronizing Access to Shared Objects
Share state is good for communication, cooperation, and sharing information among threads. However, It's more complex to handle those in real-life
## Independent and Cooperating Threads

+ Independent thread: one that can't affect or be affected by the rest of the universe. 
  + Its state isn't shared in any way by any other thread.
  + Deterministic: input state alone determines results.
  + Reproducible. 
  + Can stop and continue with no impact on behavior
+ For independent threads, the scheduling order doesn't master.
+ Cooperating threads: those that share state.
  + Behavior is nondeterministic: depends on relative execution sequence and cannot be predicted in advance. 
  + Behavior may be irreproducible.
## Problem: Too Much Milk
+ the basic problem: 
```
          Person A                       Person B
3:00      Look in fridge: no milk
3:05      Leave for store
3:10      Arrive at store                Look in fridge: no milk
3:15      Leave store                    Leave home
3:20      Arrive home, put milk away     Arrive at store
3:25                                     Leave store
3:30                                     Arrive home: too much milk!
```
+ Definitions:
  + Synchronization: using atomic operations to ensure correct operation of cooperating threads.
  + Critical section: a section of code, or collection of operations, in which only one thread may be executing at a given time. 
  + Mutual Section: Mechanisms used to create critical sections. 
> **Note**
> Typically, mutual exclusion achieved with a locking mechanism: prevent others from doing something. For example, before shopping, leave a note on the refrigerator: don't shop if there is a note. 

+ 
+ **Solution 1**: Set a flag when someone is going to buy milk and check this flag before going to buy milk. 
```
if (milk == 0){                 // if no milk
    if (note == 0){             // if no note
        note = 1;               // leave note
        milk ++;                // buy milk
        note = 0;               // remove note
    }              
}
```
*Error case*: 
```
    // Thread A                         Thread B
    if (milk==0){                       if (milk==0){
                                            if (note==0){
                                                note = 1;
                                                milk++;
                                                note = 0;
                                            }
                                        }
        if (note==0){
            note = 1;
            milk++;
            note = 0;
        }
    }
```
*output*: milk will be 2 != expected (milk == 1).
+ **Solution 2**: Use 2 variables for the notes, a roommate can create a note before checking other note and the milk then making a decision to buy.
Path A
```
noteA = 1;          //leave note
if (noteB == 0){    // of no note A1
    if (milk==0){   // if no milk A2
        milk ++;
    }
}
noteA = 0;          // remove note A
```
Path B 
```
noteB = 1;          //leave note
if (noteA == 0){    // if no note 
    if (milk==0){   // if no milk 
        milk ++;
    }
}
noteB = 0;          // remove note
```
*Error Case*: noteA and noteB can be 1 or 0 in the same time.  $\to$ No one buy milk if needed
+ **Solution 3**: 
Path A
```
noteA = 1;          // leave note A
while (noteB ==1 ){ //wait for no note B spin
    ;
}
if (milk == 0){     // if no milk
    milk++;
}      
noteA = 0;          // remove note A

```
Path B
```
noteB = 1;              // leave note B
if (noteA == 0){        // if no note A
    if (milk == 0){     // if no milk
        milk++;         // buy milk
    }      
}
noteB = 0;          // remove note B
```
*Disadvantages*: 
+ Asymmetric (and complex) code.
+ While B is waiting it is consuming resources(busy waiting)
$\to$ *solution* : [Symmetric solution without busy-waiting](https://en.wikipedia.org/wiki/Peterson%27s_algorithm)

## Structuring Shared Objects. 
+ **Shared objects**: are objects that can be accessed safely by multiple threads. 
+ All shared state in a program - including variables allocated on the heap, and static, global variables - should be encapsulated in one or more share objects. 

<div style = "text:align">
<img src = "/Media/OS/shared-objects-structure.png">
</div>

+ **Shared object layer** : define application logic and hide internal implementation details. Externally, they appear to have the same interface as you would define for a single-threaded program.
+ **Synchronization variable layer**: is a data structure used for coordinating concurrent access to shared state. 
+ **Atomic instruction layer**

## Lock Mutual Exclusion

A **lock** is a synchronization variable that provides mutual exclusion - when one thread holds a lock, no other thread can hold it.  
$\to$ Use for guarantees that one update or query completes before the next one starts.
1. **Locks: API and Properties.**
   + 2 methods: *Lock::acquire()* and *Lock::release()*
     + A lock can be in one of two states: BUSY and FREE.
     + A lock is initially in the FREE state.
     + Lock::acquire() waits until the lock is FREE and then atomically makes the lock BUSY.
     + Lock::release() makes the lock FREE. If there are pending `acquire` operations, the state change cause one of them to proceed.
   + **Lock's Properties**:
     1. **Mutual Exclusion**: At most one thread holds the lock.
     2. **Progress**: If no thread holds the lock and any thread attempts to acquire the lock, then eventually some thread succeeds in acquiring the lock.
     3. **Bounded waiting**: If thread T attempts to acquire a lock, then there exists a bound on the number of times other threads can successfully acquire the lock before T does. 
   
## Condition Variables: Waiting for a Change

**Condition Variable Definition**: is a synchronization object that lets a thread efficiently wait for a change to shared state that is protected by a lock. A condition variable has 3 methods:
   + **CV::wait(Lock *lock)**: This call atomically *release the lock and suspends execution of the calling thread*, placing calling thread on the condition variable's waiting list. Later when the calling thread is re-enabled, it *re-acquires the lock* before returning from the `wait` call
   + **CV::signal()**: This call take one thread off the condition variable's waiting list and marks it as eligible to run. If no threads are on the waiting list, `signal` has no effect.
   + **CV::broadcast()**: This call takes all threads off the condition variable's waiting list and marks them as eligible to run. If no threads are on the waiting list, `broadcast` has no effect.

## Designing and Implementing Shared Objects 

+ In concurrent code, it is not enough for the code to work. It also needs to be simple enough to understand. 
### Designing And Implementing Shared Objects: High Level Methodology.
+ A shared object has: **public methods**, **private methods**, **state variables**, and **synchronization variables**. 
  + Synchronization variables includes a lock and one or more condition variables. 
+ Steps for designing multi threaded shared objects:
  1. Add a lock: Each sahred object needs a lock as a member variable to enforce mutually exclusive access to the object's shared state. 
  2. Add code to `acquire` and `release` the lock: add `acquire` the lock at start of each public method and release it at the end of each public method. $\to$ the lock is already held when each private method is called, no need to re-acquire.  
  3. Identify and add condition variables: add condition variable for each situation in which the method must wait. 
  4. Add loops to wait using the condition variables
  5. Add `signal` and `broadcast` calls