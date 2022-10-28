# Linkers and Dynamic Linking

## Memory layout
<div style='text-align:center'>
<img src="/Media/OS/Memory-layout.png">

<figcation>**Fig 1.1**: Memory layout</figcaption>
</div>

+ **Stack**:
  +  store all data needed by a function in a program
  +  Calling a function is the same as pushing the called function execution onto the top of the stack $\to$ when function completes, the results are returned poping the function off the stack. 
  +  Data struct pushed for function is named a stack frame, it contains :
     +  Function arguments
     +  Return address
     +  Space for the local variables 
+ **Heap**: 
  + store dynamic memory allocation  $\to$ can leak memory if we forgot free after creating
+ **BSS(Block Started By Symbol)**: 
  + Uninitialized data segment, store variable is initialized by the kernel to arithmetic 0 before program starts executing. 
  + Ex: `static int i`
+ **Data**:
  + Containt initialized global and static variables which have a pre-defined value and can be modified. 
+ **Text**: Code segment
  + Where a machine language instruction is stored. 

## Linker
+ Linker is a program in a system which helps to link object modules of a program into a single object file
*Source code -> compiler -> Assembler -> Object code -> Linker -> Executable file -> Loader*
+ Functions of a linker:
  + Combine all the pieces of a program
  + Figure out a new memory organization so that all the pieces fit together.
  + Touch up addresses sos that the program can run under the new memory organization.
$\to$ a runnable program stored in a object file called an executable.

+ 2 types of linkers: https://www.geeksforgeeks.org/linker/
  + Static linker: 
  + Dynamic linker:
