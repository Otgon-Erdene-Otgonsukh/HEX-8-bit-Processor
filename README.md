## 🔲 Hex 8-bit Processor

This repository contains a HEX 8-bit processor designed in a java simulation environment called *ModuleSim* which contains pre-built architectural modules unlike *Logisim* allowing for abstraction and more cleaner approach to building logical units. The design was part of the Computer Architecture course in University of Bristol. 

The built CPU is capable of executing 16 instructions and regarded as RISC type due to it having simple and mostly register-to-register instructions with the exception of a few loading and storing values from an to a memory which is included in the design and the instructions are fetched from the memory and can be loaded with custom sequence of instructions via a `.hex` file upload.

## Core Components

The processor design consists of **4 main** components including:

 - Timing Unit
 - Instruction Decoder
 - Control Unit
 - Calculation Unit

### Timing Unit

<img width="382" alt="Screenshot 2026-05-17 211305" src="https://github.com/user-attachments/assets/e9b554ea-45bf-49b8-b0c2-ab35cbb589ee" />

The timing unit contains a clock component which is used to synchronize the updating of the registers and to cycle between the 4 main execution cycle of the CPU which are: 
 - Fetch
 - Decode / Increment PC
 - Execute
 - Write Back

Each cycle takes one full clock cycle and repeats, continuously fetching instruction from the memory and executing them. The Demultiplexer unit represents the 4 main cycle and sends a signal from the appropriate output to the corresponding unit which is noted above.

### Instruction Decoder

<img width="356" alt="Screenshot 2026-05-17 213636" src="https://github.com/user-attachments/assets/a8c6f619-cf17-45fd-bd24-f040ce7aa392" />

The 2-layer Demultiplexers take in the Decode signal from the timing unit and sends that active signal to the correspondign output out of the 16 total output available on the right side. The instruction bit code is retrieved from the `instruction register (4 bit)` and is connected to the control signal input of the demuxes.

### Control Unit

<img width="563" alt="Screenshot 2026-05-17 214128" src="https://github.com/user-attachments/assets/665ecea1-df7e-4562-b028-54e70f7877b5" />

The control unit is a collection of `OR` modules that is used in conjuction to send the correct activation signals that were outputted from the instruction
decoder for each instruction. Those collective signals are used to activate the correct computationol units of calculation component needed for the current instruction to be executed. 

### Calculation Unit

<img width="510" alt="Screenshot 2026-05-17 214449" src="https://github.com/user-attachments/assets/6f181f5a-b4e5-4159-9a02-ceda2c15e475" />

This is the section where the `memory` and `registers` are placed to hold the instruction and data and values needed for computation. Multiplexers are used to select the correct register and Arithmetic and logical unit (ALU) is present to perform computation and comparison for `conditional branching` which is also supported by the instruction set architecture (ISA).

## Guide on Running the Simulation

The CPU is designed in the Java based tool for designing architectural layouts called `ModuleSim`
