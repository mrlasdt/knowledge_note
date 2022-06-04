# Introduction

## 1.1 What Operating System Do
+ An **operating system** is software that manages a computer's hardware. 
+ A computer system can be divided roughly into four components
  + *Hardware*: the central processing unit(CPU), the memory, the I/O devices
    + Role: Provide the basic computing resources for the system
  + *Operating system*: 
    + Role: control hardware and coordinates its use among the various application programs for various users.
  + *Application programs*:
    + Role: define the ways, in which resources are used to solve user's computing problems.
  + *user*
  ### 1.1 User View
  + The user’s view of the computer varies according to the ***interface being used*.**
  $\to$ Goal: Os as a system designed to maximize works that the user is performing. 
  + Objective:
    + ease of use
    + with some attention paid to performance and security.
    + None paid to resource utilization. 

### 1.1.2 System View
+ the operating system is the program most intimately involved with the hardware. 
$\to$ Operating system as a ***resource allocator***

### 1.1.3 Defining Operating Systems
+ The common functions of controlling and allocating resources are then brought
together into one piece of software: the operating system.
$\to$ we have no completely adequate definition of an operating system
+ Operating system is the one program running at all times on the computer—usually called the
***kernel***

+ There are two other types of programs: 
  + *System
programs*: which are associated with the operating system but are not necessarily part of the kernel
  + *Application programs*, which include all programs not associated with the operation of the system
> Inclusion:
> +  Goal of OS: Convenience and efficiency
>+ Function of OS: 
>   + it is an interface between user and hardware
>   + Allocation resources
>   + Management of memory, security. etc..

## 1.2 Computer-System organization

<div style = "text-align:center">
<img src="/Media/computer_system.png">
</div>

+ A modern general purpose computer system consists of one or more CPUs and a number of device controllers connected through a common bus that provides access to shared memory.
  + Each device controller is in charge of a specific type of device
  + The CPU and the device controllers can execute concurrently, competing for memory cycles
  + To ensure orderly access to the shared memory controller is provided whose function is to synchronize access to the memory. 

## 1.3 Events and Interrupt
+ **Bootstrap Program**: 
  + The initial program that runs when a computer is powered up or rebooted
  + It is stored in the ROM(Read only memory)
  + It must know how to load the OS and start executing system.
  + It must locate and load into memory the OS Kernel
+ **Interrupt**:
  + The occurence of an event is usually signalled by an Interrupt from Hardware or Software
  + Hardware may trigger an interrupt at any time bt sending a signal to the CPU, usually by the way of the system bus.
+ **System call(Monitor Call)**: 
  + Software may trigger an interrupt by executing a special operation called System call

**How interrupt work**
<div style = "text-align:center">
<img src="/Media/how_interrupt_work.png">
</div>
+ When the CPU is interrupted, it stops what it is doing and immediately transfers execution to a fixed location. The fixed location usually contains
the starting address where the service routine for the interrupt is located.
+ The interrupt service routine executes;
+ On completion, the CPU resumes the
interrupted computation.


## 1.4 Storage

## 1.5 I/O structure


# Computer System Architecture
## 1.1 Single-processor systems

## 1.2 Multiprocessor Systems.

