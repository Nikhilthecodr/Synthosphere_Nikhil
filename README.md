# Synthosphere
Synthosphere is a hackathon project.It involves creating Verilog code to describe circuit behavior (pre-synthesis) and then translating it into optimized gate-level representations (post-synthesis) using synthesis tools. 

__Name: Nikhil H Raju__

__USN: 1BM21EC088__
# 16-bit single cycle MIPS Processor

A 16-bit single-cycle MIPS processor is a simplified computer processor that operates on 16-bit data and instructions. It executes each instruction in just one clock cycle, making it straightforward but potentially limiting in terms of performance. This processor includes a basic set of components like registers, an arithmetic logic unit (ALU), a control unit, memory units for instructions and data, and a simple pipeline for instruction fetch, decode, execute, memory access, and write-back stages.

![image](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/assets/111330348/a8701511-3670-47b0-8841-65e8528316db)

__Instruction Set of 16-bit MIPS Processor__
```
LW: Load Word - Load a 16-bit value from memory into a register.
SW: Store Word - Store a 16-bit value from a register into memory.

Arithmetic and Logic Instructions:
ADD: Add - Add two registers and store the result in a destination register.
SUB: Subtract - Subtract one register from another and store the result.
AND: Bitwise AND - Perform bitwise AND operation between two registers.
OR: Bitwise OR - Perform bitwise OR operation between two registers.
XOR: Bitwise XOR - Perform bitwise XOR operation between two registers.

Control Transfer Instructions:
BEQ: Branch if Equal - If two registers are equal, branch to a specified address.
BNE: Branch if Not Equal - If two registers are not equal, branch.
J: Jump - Unconditionally jump to a specified address.

Immediate Instructions:
ADDI: Add Immediate - Add a constant value to a register.
ANDI: Bitwise AND with Immediate - Perform bitwise AND operation with a constant.
ORI: Bitwise OR with Immediate - Perform bitwise OR operation with a constant.

Shift Instructions:
SLL: Shift Left Logical - Shift the bits of a register left by a specified amount.
SRL: Shift Right Logical - Shift the bits of a register right by a specified amount.
```
# Block Diagram

![image](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/assets/111330348/c362af84-479c-4c02-856f-5fd6fb52ec5a)

__RTL of all the modules__
* Program links:-
     1. [ALU Unit](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/blob/main/alu.v)
     2. [ALU Control Unit](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/blob/main/alu_unit.v)
     3. [Control Unit](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/blob/main/control_unit.v)
     4. [Data Memory Unit](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/blob/main/data_memory.v)
     5. [Instruction Set](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/blob/main/instruction.v)
     6. [Register file](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/blob/main/register.v)
     7. [Main module processor](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/blob/main/processor.v)

__Test Bench__:

   1. [Test Bench of Processor](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/blob/main/tb_processor.v)

Iverilog and gtkwave codelines(Presynthesis):
```
- iverilog <filetop.v> <file1.v> …. <tb_filetop.v>
- ./a.out
Copy the generated dumpfile.vcd and run it with
- gtkwave dumpfile.vcd
```
__RTL Simulation Waveform__

![image](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/assets/111330348/3c411e04-21fd-4872-97a9-7020704dbbe3)

__Synthesis__

 Flow for synthesis
 ```
yosys
read_liberty -lib <relative or abs path>/ lib file 
read_verilog <verilog_file.v>
synth -top <verilog_file> 
abc -liberty <relative or abs path>/ lib file ( generates results on ur design → netlist verify them before continuing)
show 
write_verilog <file_name>.v  OR    write_verilog -noattr  <file_name>.v 
```

The standard cells were invoked when mapped to the standard library file

![image](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/assets/111330348/14767b66-45bd-4287-8688-77a6b5b714b1)

__Sythesized Netlist File__

 [Synthesized Netlist of all modules](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/blob/main/sythesized_netlist_processor.v)

__Design Hierarchy__

![image](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/assets/111330348/ba1ee7c5-0dbb-42b5-9d3a-87af3247e231)

![image](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/assets/111330348/7b4dd459-77f0-4121-b2c6-a0e329586aeb)

![image](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/assets/111330348/87cd52b6-6c04-4511-9e67-52e302eb5870)

![image](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/assets/111330348/12d7ac41-4814-403f-ba7f-a158b2331337)

__Synthesis output__

MIPS Processor

![image](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/assets/111330348/500800f9-e693-41f1-a8b4-70ea236263d2)

ALU Control Unit

![image](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/assets/111330348/1ed3e0f3-688d-4081-bf50-81f9eba95f4c)

__GLS Simulation Result__

![image](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/assets/111330348/3448e83d-30a5-4cc9-9d45-4a04ab8aff5d)

The functionality of the PWM generator with variable duty cycle is retained post-synthesis. Hence the deisgn does not have Simulation-Synthesis Mismatch














