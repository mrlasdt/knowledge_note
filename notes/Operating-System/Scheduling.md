# Scheduling

## Performance terminology
+ **Task**(also called job): a user request.
+ **Response time**(or delay): The user-perceived time to do some task.
+ **Predictability**: Low variance in response times for repeated requests.
+ **Throughput**: the rate at which tasks are completed.
+ **Scheduling overhead**: The time to switch from one task to another.
+ **Fairness**: Equality in the number and timeliness of resources given to each task. 
+ **Starvation**: the lack of progress for one task, due to resources given to a higher priority task. 



## 1. Uni-processor Scheduling
+ Three simple well-known policies:
  + First in first out. (first come first served)
  + Shorted job first.
  + Round robin.
### 1.1 First-in-first out 
+ Do each task in the order in which it arrives. 

<div style='text-align:center'>
<img src="/Media/OS/scheduling/FIFO.png">
<figcaption >**Fig1**. Comparing FIFO and SJF</figcaption>
</div>

+ **Advantages** :
  + Minimize overhead(time switching between tasks). $\to$ because it only switch when task completed/
  + Best throughput: complete task quickly because it not share processor for another tasks.
  + Fairness: every task patiently waits its turn.
+ **Disadvantages**: 
  + if a task take a long time $\to$ another task will be wait until previous task ended. $\to$ average response time maybe high.

### 1.2 Shortest Job First (SJF)
+ shorted task mean the time remaining of processing the task is the smallest.
+ **Advantages**: 
  + Minimize average response time.
+ **Disadvantages**:
  + Long task will be delayed or never completed.
  + Maybe suffer from starvation and frequent context switches.

### 1.3 Round Robin.
+ Tasks take processor in a limited period time. 
<div style="text-align:center">
<img src="/Media/OS/scheduling/RR.png">
<figcaption>**fig 2**. Round Robin scheduling</figcaption>
</div>

+ **Advantages**: 
  + There is no possibility that a task will starve.
+ **Disadvantages**: 
  + Overhead time is high due to many time switching between tasks.
### 1.4  Multi-Level FeedBack Queue(MFQ)
+ MFQ is designed to achieve several simultaneous goals:
  + **Responsiveness**: run short tasks quickly, as in SJF.
  + **Low overhead**: Minimize the number of preemptions, as in FIFO, and minimize the time spent making scheduling decisions.
  + **Starvation-Freedom**: all tasks should make progress, as in Round-Robin.
  + **Background Tasks**: Defer system maintenance tasks, such as disk defragmentation so they do not interfere with user work.
  + **Fairness**: Assign (non-background) processes approximately their max-min fair share of the processor.



<div style='text-align:center'>
<img src ='/Media/OS/scheduling/RR-mechanism.png'>
</div>

+ Mechanism:
  + Using multiple Round-robin queue with a different priority level and time quantum. 
  + Tasks at a higher priority level preempt lower priority tasks, tasks with the same priority will be scheduled in Round-Robin mechanism. 
  + Tasks are moved between priority levels to favor short tasks over long ones $\to$ tasks uses up its time $\to$ drop its level $\to$ repeat until it completed and leave system.

## 2. Multi-processor Scheduling
