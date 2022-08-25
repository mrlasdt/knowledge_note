# Concurrency

+ Thread: set of streams of execution. 
+ Each thread behaves as if it has its own dedicated processor.
+ The operating system provides the illusion that programmers can create as many threads as they need and each thread runs on its own dedicated virtual machine. In reality, a machine only has a finite number of processors, and it is the operating system's job to transparently multiplex threads onto the actual processors.
+ 
+ **Threads abstraction** lets the programmer create as many threads as needed 
<div style= "text-align:center">
<img src = "/Media/OS/threads.png">
<figcaption> **Figure 1.1** : OS organized threads created by programmers to actual processors. </figcaption>
</div>

# Threads

+ A thread is a *single execution sequence* that represents a *separately schedulable tasks*.
  + **Single execution sequence**: Each thread executes a sequence of instructions - assignments, conditionals, loops, procedures and so on - just as in the familiar sequence programming model.
  + **Separately schedulable task**: The operating system can run, suspend, or resume a thread at any time. 
+ A thread scheduler scheduled(running, suspending and resuming) between running threads $\to$ create illusion of processing task parallel $\to$ threads run on a dedicated virtual processor with *unpredictable and variable speed*.

<div style  = "text-align:center">
<img src = "/Media/OS/thread_scheduler.png">
<figcaption>**Figure 1.2**: Three possible ways that a thread might execute, all of which are equivalent to the programmer.</figcaption>
</div>


<div style  = "text-align:center">
<img src = "/Media/OS/thread_scheduler_2.png">
<figcaption>**Figure 1.3**: Some of the many possible ways that three threads might be interleaved at runtime</figcaption>
</div>

+ **Cooperative vs. preemptive multi-threading**:
    + **Cooperative threads**: a thread runs without interruption until it explicitly relinquishes control of the processor to another thread. 
      + Advantages: Increased control over the interleaving among threads.
        + For example: in most cooperative multi-threading systems, only one thread runs at a time, so while a thread is running, no other thread can run and affect the system’s state.
      + Disadvantages: A long run-thread may hold resource and another threads do not have resource to use.
    + **Preemptive multi-threading**: threads can be switched at anytime. 
## Thread Data Structures
+ Thread Data Structures used for saving thread's state $\to$ for switching processors during process.


<div style = "text-align:center">
<img src = "/Media/OS/thread_state.png">
<figcaption>**Figure 1.4**: Thread Data Structures</figcaption>
</div>

### Per-Thread State
+ **Thread Control Block (TCB)** is where OS allocate space for current state of each thread's computation. TCB included:
    1. The state of the computation being performed by the thread. (stack information and saved registers)
       + **Stack**: Stored information(variables, parameters, function ...) needed by the nested procedures of running thread.
       + **Copy of processor registers**: 
         + Stored intermediate value for ongoing computation.
         + Stored special-purpose registers such as the instruction pointer and stack pointer. Ex: stop and re-run thread on the top of the stack.
    2. Metadata about the thread that is used to manage the thread.
### Shared State
+ Per-thread state is allocated for each thread, *some state is shared between threads running in the same process or within the operating system kernel*
  + Ex: program code is shared by all threads in a process, although each thread may be executing at a different place within that code.


## Thread Life Cycle

<div style = "text-align:center">
<img src = "/Media/OS/thread_life_circle.png">
<figcaption>**Figure 1.5**: The states of a thread during its lifetime</figcaption>
</div>
  
<div style = "text-align:center">
<img src = "/Media/OS/thread_location_in_different_state.png">
<figcaption>**Figure 1.6**: Location of thread's per-thread state for different life cycle stages</figcaption>
</div>
 
  