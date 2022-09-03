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
