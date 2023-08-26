# Synthosphere
Synthosphere is a hackathon project. It involves creating Verilog code to describe circuit behavior (pre-synthesis) and then translating it into optimized gate-level representations (post-synthesis) using synthesis tools. 

__Name: Nikhil H Raju__

__USN: 1BM21EC088__
# 16-bit single cycle MIPS Processor

A 16-bit single-cycle MIPS processor is a simplified computer processor that operates on 16-bit data and instructions. It executes each instruction in just one clock cycle, making it straightforward but potentially limiting in terms of performance. This processor includes a basic set of components like registers, an arithmetic logic unit (ALU), a control unit, memory units for instructions and data, and a simple pipeline for instruction fetch, decode, execute, memory access, and write-back stages.

![image](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/assets/111330348/a8701511-3670-47b0-8841-65e8528316db)

### Instruction set

| Instruction       | Operation                   | Description                                                                           |
| ----------------- | --------------------------- | ------------------------------------------------------------------------------------- |
| add rd, rs, rt    | rd = rs + rt                | rd = destination, rs, rt = source                                                     |
| sub rd, rs, rt    | rd = rs – rt                | rd = destination, rs, rt = source                                                     |
| mult rs, rt       | hi;lo = rs*rt               | hi, lo: two 16-bit registers in multiplier unit to store 32-bit multiplication result |
| and rd, rs, rt    | rd = rs & rt                | rd = destination, rs, rt = source                                                     |
| or rd, rs, rt     | rd = rs \| rt               | rd = destination, rs, rt = source                                                     |
| addi rd, rs, I    | rd = rs + I                 | rd = destination, rs = source, I = 16-bit immediate value                             |
| sll rd, rs, shamt | rd = rs << shamt            | rd = destination, rs = source, shamt = shift amount                                   |
| slt rd, rs, rt    | rd = (rs < rt)              | rd = 1 if rs < rt, otherwise rd = 0                                                   |
| mfhi rd           | rd = hi                     | Load hi from multiplier unit into register rd                                         |
| mflo rd           | rd = lo                     | Load lo from multiplier unit into register rd                                         |
| lw rd, i(rs)      | rd = rs[i]                  | rd = destination, rs = base address, i = offset                                       |
| sw rs, i(rd)      | rd[i] = rs                  | rd = base address, rs = source, i = offset                                            |
| beq rs, rt, label | if (rs == rt) jump to label | rs, rt = registers to compare, label = label to jump to                               |
| blez rs, label    | if (rs <= 0) jump to label  | rs = register to compare, label = label to jump to                                    |
| j label           | Jump to label               | label = label to jump to                                                              |
| adds rd, rs, I    | rd = rs + I                 | rd = address, rs = source, I = 16-bit immediate value                                 |

### Block Diagram

![image](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/assets/111330348/c362af84-479c-4c02-856f-5fd6fb52ec5a)

### RTL of all the modules
* __Program links:__
     1. [ALU Unit](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/blob/main/alu.v)
     3. [ALU Control Unit](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/blob/main/alu_unit.v)
     4. [Control Unit](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/blob/main/control_unit.v)
     5. [Data Memory Unit](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/blob/main/data_memory.v)
     6. [Instruction Memory](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/blob/main/instruction.v)
     7. [Register file](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/blob/main/register.v)
     8. [Main module processor](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/blob/main/processor.v)

### Test Bench:

 * [Test Bench of Processor](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/blob/main/tb_processor.v)

## RTL Simulation

### Tools used

1. __Icarus Verilog (iverilog):__ Open-source HDL simulator for digital circuit testing.

2. __GTKWave:__ Open-source waveform viewer for simulation results analysis.

### Iverilog and gtkwave codelines:
```
- iverilog <filetop.v> <file1.v> …. <tb_filetop.v>
- ./a.out
Copy the generated dumpfile.vcd and run it with
- gtkwave dumpfile.vcd
```
### RTL Simulation Waveform

![image](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/assets/111330348/3c411e04-21fd-4872-97a9-7020704dbbe3)

## Synthesis
### Tool used

__Yosys:__ Open-source synthesis tool for designing digital circuits. Transforms RTL code into optimized gate-level representation.

### Flow for synthesis
 ```
yosys
read_liberty -lib <relative or abs path>/ lib file 
read_verilog <verilog_file.v>
synth -top <verilog_file> 
abc -liberty <relative or abs path>/ lib file ( generates results on ur design → netlist verify them before continuing)
show 
write_verilog <file_name>.v  OR    write_verilog -noattr  <file_name>.v 
```

The following standard cells were invoked when mapped to the standard library file

![image](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/assets/111330348/14767b66-45bd-4287-8688-77a6b5b714b1)

### Synthesized Netlist File

 * [Synthesized Netlist of all modules](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/blob/main/sythesized_netlist_processor.v)

### Design hierarchy and number of instances

![image](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/assets/111330348/ba1ee7c5-0dbb-42b5-9d3a-87af3247e231)

### Detailed analysis:

* [Number of cells and instances](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/blob/main/Number_of_cells.txt)


## Synthesized design

Used ```opt -purge``` command to remove unused modules and objects from a Verilog design during synthesis, optimizing the design's size and complexity.

__MIPS Processor__

![image](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/assets/111330348/ba0d3909-ba86-4cec-8227-c51d2ce823f0)

__Instruction Memory__

![image](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/assets/111330348/6b5eab0b-2b2c-4ccd-9895-cbeaceb3262d)


__ALU__

![image](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/assets/111330348/d35d5b60-f0e3-4c98-9d93-321e5eeaf4df)


__Control Unit__

![image](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/assets/111330348/127cb761-2b82-4719-b4a3-8e96471d92cf)


### GLS Simulation Result

![image](https://github.com/Nikhilthecodr/Synthosphere_Nikhil/assets/111330348/3448e83d-30a5-4cc9-9d45-4a04ab8aff5d)

The behavior and functionality of the 16-bit single-cycle MIPS Processor are successfully preserved after the synthesis process, ensuring that there is no disparity between the design's performance in simulation and its behavior in the synthesized hardware. This indicates that the synthesized design accurately represents the intended processor functionality, and any potential simulation-synthesis mismatch has been effectively mitigated.













