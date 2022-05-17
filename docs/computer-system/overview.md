---
sidebar_position: 1
---

# Overview

## Introduction

In this root section we'll take a closer look at how computer systems work and what are the pieces that compose it.

This knowledge of low-level concepts can be a difference maker for the programmer, by understanding it, one can have a clearer mental model of how programs run on a machine, how to improve the performance of a program, how to catch some nasty bugs, and how to write more secure code. Overall, the programmer after grasping these concepts, will have a more fundamental and solid knowledge of his craft, understanding more holistically the computer system and how to leverage it to write better code and create better abstractions.

On this particular chapter, we'll have a tour through computer systems by taking a close look to the following program:

```c
#include <stdio.c>

int main()
{
  printf("Hello, World!\n");
  return 0;
}
```

## Information is Bits + Context

On computer systems, information is nothing but bits + context. Bits are 1s and 0s, and are grouped into chunks of 8 called _bytes_.

To illustrated what was state above, a byte can represent a character "a", or it can represent a number "1", it all depends on the context of which the data is being viewed.

Groups of bytes can be viewed together to form larger information structures such as words, or paragraphs.

To reference our _hello_ program, each character is represented by a byte. Files that use exclusively the ASCII characters are called _text files_ and all other files are binary files.

## Programs are Translated by other Programs into Different Forms

The way the human brain interprets information and the way machines interpret information differ greatly. Machines like 1s and 0s, while we prefer something more semantic and meaningful. This generates a substantial barrier when it comes to computers systems and writing software.

We humans like to write code that we can easily understand, but the computer needs the program in a format that it can run. For that we have programs that translate other programs into different forms.

Take our _hello_ program for example, it's humanly readable (at least partially...), we put it through a compilation system and it spits out an executable, which is machine-friendly file ready to be run.

The C compilation system (usually gcc) is composed of:

- _Pre-processor_: Which takes the directives that begin with the # character and update the program to replace it with the values
- _Compiler_: Turns the pre-processed program into assembly. Assembly is useful because it allows different languages to compile to the same output.
- _Assembler_: translates the program into machine-level instructions
- _Linker_: Links up the library and all the files that compose the program, handling all the merging.

The result is an executable, in this case a _hello_ executable.

## It Pays to Understand How Compilation Systems Work

Most of the time, and in most cases, we don't really need to understand how the compilation system does it's job, we write our code, throw it at the compiler and it spits out optimized machine code. However, there are cases in which it is very valuable to understand compilation systems:

- _Optimizing program performance_: By understanding how the compiler does it's job, you can write 'compiler-friendly' code which will result on the compiler being able to optimize the code better
- _Understanding link-time errors_: Some of the nastiest bugs to debug are link time errors, they can occur at any point in development. By understanding compilation and linking, we can try and prevent this bugs better, and catch them more rapidly if they creep into the code.
- _Avoiding security wholes_: Buffer overflow vulnerabilities have plagued security of many network programs and servers. This is partially because too few programmers understand how the stack works and how the compilation process influences that, and so they aren't very strict with the data that the program takes in from untrusted sources.

## Processors Read and Interpret Instructions Stored in Memory

Processors are at the heart of computers systems. A processor or central processing unit (CPU) is responsible for carrying out machine-level instructions of a program loaded in main memory.

To better understand how our _hello_ program runs, we must take a look at the typical hardware organization of a computer system.

### Hardware Organization of a System

![Computer Systems Hardware Organization](/img/docs/computer-systems-hardware-organization.jpeg)

#### Buses

Hardware buses are like channels where bytes travel between hardware components, connecting them.

#### I/O Devices

I/O devices are the connection of a computer system to the outside world, with them the system receives user input and outputs data, essentially the artifacts that the system uses to interact with it's outside environment.

#### Main Memory

The main memory is a temporary storage device that holds both a program and the data it manipulates while the processor is executing that program.

Physically, main memory consists of a collection of _dynamic random access memory_ (DRAM). Logically, main memory is organized as a linear array of bytes, each with its own unique address (array index) starting at zero.

#### Processor

Processors or CPUs are the engine responsible for interpreting and executing instructions stored in main memory, they are usually composed of a special register called _program counter_ (PC), a _register file_, an _arithmetic logical unit_ (ALU) and a bus interface.

The PC points to a instruction in main memory. Processor instructions are defined by its _instruction set architecture_. Instructions execute in a strict sequence, and executing an instruction involves performing a series of steps. The processor reads the instruction from memory pointed at by the PC, interprets the bits of the instruction, performs some simple operation dictated by the instruction and updates the PC to the next instruction in the program.

This simple operations revolve between the main memory, the register file, and the ALU. The register file is a small storage device, and the ALU computes new data and memory addresses values. Some of this simple operations are:

- _Load_. Copy a value from an address at main memory into a register in the register file.
- _Store_. Copy a value from a register into main memory.
- _Operate_. Compute a value from two values stored on registers
- _Jump_. Copy a value into the PC, jumping jumping instructions.

### Running the hello Program

With this new knowledge about a computer system's hardware organization, let's take a look at how our _hello_ program runs.

First, the shell program is executing it's instructions, waiting for us to type a command. We then type _./hello_, this starts a process that copies our executable file from disk into main memory. Once in main memory, the PC register can is updated to point to the address at the start of the instruction set of our program (which is now machine code). The processor then starts executing the instructions, it copies the string "Hello, World!\n" (which is now just a bunch of bytes), into one of it's registers, and then it proceeds to copy that over to the screen I/O device, outputting the value for us!

## Caches Matter

You may have notice that a lot of the efforts of the system are used moving data around components. As you may deduce, this can get expensive for performance, and so caches can substantially improve the performance of the system.

The thing about memory is that the bigger it is the slower it gets, and the smaller it is the pricier it gets. And so caches are usually implemented in the processor in different levels: L1, L2, and L3.

L1 serves as a cache for the registers, L2 serves as a cache for L1, L3 for L2, and L3 serves as a cache for main memory.

## Storage Devices Form a Hierarchy

This memory configuration forms a memory hierarchy, the higher up the hierarchy the more expensive the memory device gets, but the faster it is by huge orders of magnitude.

![The Memory Hierarcht](/img/docs/memory-hierarchy.jpeg)

## The Operating System Manages the Hardware

The operating system serves as a layer between the hardware resources and the program. It doesn't allow the program to access hardware directly, any attempt to manage hardware must go through the operating system kernel.

The operating system has two primary purposes: (1) to protect the hardware from misuse by runaway applications and (2) to provide applications with simple and uniform mechanisms for manipulating complicated and often wildly different low-level hardware devices. The operating system achieves both goals via the fundamental abstractions of: _processes_, _virtual memory_, and _files_.

### Processes

When our _hello_ program is running, the operating system provides the illusion that it's the only program running on the hardware. That's the great abstraction of processes, each process can be thought as if it owns all the hardware resources when executing, and so it doesn't have to worry about other programs.

In reality multiple processes can and more often than not, do run concurrently in a system. It's the job of the operating system to ensure that this is handled properly. If the system has only one processor, the kernel can create alternate processes in the processor, giving the illusion that they are all running at the same time, when in fact they are taking turns very rapidly. If the system has multiprocessors, than multiple process can truly run in parallel.

#### Threads

A process can consist of multiple execution units, called threads, each running in the context of the process and sharing the same global data. Threads are increasingly important for network servers, because its easier to share data between threads compared to sharing between processes, and they are lighter too. Multi-threading is also another way of leveraging multiple processors for performance.

### Virtual Memory

Virtual memory provides an abstraction upon the hardware physical main memory. It gives a process the illusion that he has the entire memory for itself, and shields a process' memory from others. This virtual memory address space consists of the program code and data, the heap, shared libraries, the stack, and the kernel virtual memory (which is hidden from the process). We'll go into greater detail of each one further on.

### Files

File is a sequence of bytes, nothing more, and nothing less. Every I/O device is modeled as a file, including the network interface.

This provides a great abstraction as very different hardware devices can be treated in the same way, greatly reducing complexity and provides a uniform view over all I/O devices included in the system.

## Systems Communicate with other Systems Using Networks

So far, we've seen computer systems as isolated pieces of hardware and software, but computers systems interact with each other, and they do so using networks.

[An entire section has been dedicated to this](../computer-networking/introduction.md), but for our context, data coming from or going to the network can be viewed just as another I/O device, which is abstracted as a file.
