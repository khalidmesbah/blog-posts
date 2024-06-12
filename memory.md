---
type: notes
title: memory
description: how memory works
tags:
  - fundamentals
lastmod: 2023-09-02
published: true
---

## what's

- memory: an array of bytes within RAM
- memory block: a single unit (byte) within memory, used to hold some value
- memory address: the address of where a memory block is allocated

## memory layout in C

It's organized in the following fashion
- empty space -> high address | -> command-line arguments and environment variables
- stack segment
- heap segment
- uninitialized data segments (bbs)| -> initialized to 0 by execution
- initialized data segments        | -> read from program file by execution
- text/code segment -> low address | -> read from program file by execution

### text/code segment

- contains machine code of the compiled program
- shareable so that only a single copy needs to be in memory
- often read-only, to prevent programs from accidentally modifying its instructions

### initialized data segment

- stores all initialized global and static variables

### uninitialized data segment

- often called the `bbs` (block started by symbol)
- stores all uninitialized global and static variables
- data is initialized by the kernel to arithmetic 0 before the program starts executing
  - int,float,double => 0
  - pointer => null
  - char => the null character('0' or '\0' or simply NULL)

### heap segment

- free memory available for programmers to use
- where dynamic memory allocation usually takes place
- managed by `malloc`, `realloc`, and `free`
- the implementation of the heap varies
- called dynamic memory
- using the heap is called dynamic memory allocation
- has nothing to do with the heap data structure unlike the stack segment which is an implementation of the stack abstract data type
- it's not an implementation of the heap data structure unlike the stack segment

### stack segment

- holds
  - local(automatic) variables
  - temporary information
  - function parameters
  - return address
- grows downward
  - items deeper in the call chain are ate numerically lower addresses and toward the heap
- when the stack pointer meet the heap pointer, free memory is exhausted and results in a stack overflow error
- this is how the recursive functions in c works, each time a recursive function calls itself, a  new stack frame is used, so one set of variables doesn't interfere with the variables from another instance of the function
- the size of the stack is will be decided by the operating system and the compiler

### empty space

- reserved to command-line arguments and environment variables

## example

```c
s[] = "helloworld" // initialized data segment
char *s = "helloworld" // initialized data segment
static int i; // uninitialized data segment
static in i = 10; // initialized data segment
int i; // uninitialized data segment
int i = 10; // initialized data segment
a()->b()->a()->b() // stack segment
malloc() // heap segment
```

## types of memory allocations
- static memory allocation
- dynamic memory allocation

## static memory allocation

- memory allocated during compile time
- fixed and cannot be increased or decreased during run time
- it happens in the stack segment

## dynamic memory allocation

- memory allocated at run time
- it takes place in the heap segment
- pointer play an important role in dynamic memory allocation
- allocated memory can only be accessed through pointers
- built in functions to allocate or deallocate memory in the heap
  - using c
    - `malloc` `calloc` `realloc` `free`
  - using c++
    - `malloc` `calloc` `realloc` `free` `new` `delete`

## heap vs stack segments

- stack segment is where memory is allocated or deallocated in a defined order
- heap segment is where memory is allocated or deallocated randomly without any order

## notes

- you can't control any segment of the memory layout except the heap segment

