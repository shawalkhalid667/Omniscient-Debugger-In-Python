# Omniscient-debugger-in-python

# Problem Statement:

Omniscient Debugging (also called Time Travel Debugging or Reverse Debugging) allows programmers to step back in time when debugging their code. 

Omniscient debuggers save developers’ time by obviating the need for repetitive reruns that they have to perform in order to narrow down a program fault using an error symptom. 

# Motivation:

Debugging is a challenging and time-consuming process for software developers.

Despite advances in debugging tools, upto 80% of the development costs are spent on discovering and isolating program faults

It is very common for developers to have to iteratively rerun the program with different breakpoints in order to isolate the fault.

# Methodology:

Our implementation uses a tracer/tracee model, Tracer can use PTrace to manipulate tracee’s registers, stack and instructions

# Debuggers work as follows:
User specifies a line to add a breakpoint to
ELF binaries have a DWARF section containing debugging information (symbols, line mappings etc)
Source line to assembly instruction mapping can be found in DWARF section
Python is interpreted (no elf). We use cython to transpile to c the c to ELF
Debugger will fork and start the tracee as a child process using execve() with ptrace TRACEME flag, allowing the program to be traced.
At runtime, we swap out the original assembly instruction with a one byte instruction to generate a software interrupt. (0xCC, or int 3)
How are debuggers made omniscient (state capture, scaling issues, record and replay, syscalls)

# Implementation:

Since debugger needs to capture state after every instruction, it needs to interrupt after every instruction resulting in frequent context switches.
Python to c back to python several times for each debugging step accumulates quickly
Other sources of overhead
Ptrace is a libc function, we need to interface with c code
Data types need to be converted at each call

# Conclusion:

Providing developers with the ability to create a line-by-line execution. 

Enabling developers to debug both forward and backward with the help of time travel debugging. 

With the help of ptrace access to the complete stack being used by program.








