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
