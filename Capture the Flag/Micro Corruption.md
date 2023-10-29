# Micro corruption

## Cheat sheet

### Registers

### Live Memory Dump

### Assembly Notes
#### Instructions
There are only two types of instructions.  These are either arithmatic like 'add' and control transfer, which decide what the next instruction is going to be.

Assembly programs are made of individual instructions.  Instructions typically take the form:

opcode source, destination

Source and destinsation refer to registers, constants or memory locations.  

As an example:

add #10 r15

This instruction means: r15 = r15 + 10

Arguments to instructions can have one of the following forms:

Rx - Reference to the value stored in Rx directly
@Rx - 

#### Registers
Registers are the working state of the cpu

#### Program Counter
The program counter is a special register that holds the address of the next instruction to run.

#### Stack Pointer
The stack pointer is another special register that identifies a specific region of memory carved out in temporary storage.

#### Memory
Memory, which stores the state of the program.

#### CPU Flags
The CPU flags record things like whether the last instruction produced a 'zero' or set the 'sign' flag and are used to implement the logic.




