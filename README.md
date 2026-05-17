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

The CPU is designed in the Java based tool for designing architectural layouts called `ModuleSim` which the java package for can be found in the root of the repository called [`ModuleSim.jar`](/ModuleSim.jar). You can download the jar file from this repository or from the official repository [here](https://github.com/TeachingTechnologistBeth/ModuleSim) and navigate to the `Releases` tab and download the latets release.

After downloading the java package file for the ModuleSim program, make sure you have installed a java SDK on your machine which contains the JVM that is needed to execute the `jar` file. When you have installed and setup the java SDK, run the following:

``` sh
java --add-opens java.desktop/sun.awt=ALL-UNNAMED -jar /path/to/your/downloaded/ModuleSim.jar 
```

The `--add-opens` flag is needed to allow access for the package file to an internal java package which is not public by default.  

You should now see a window similar to the following open up:

<img width="819" alt="Screenshot 2026-05-17 220532" src="https://github.com/user-attachments/assets/484f598c-1374-445d-b786-78c4699563c4" />

---
Now download the [`hex.modsim`](/hex.modsim) file from the repository which contains the actual design and after downloading, navigate to the top left menu and click the `File` tab and select `Open` and select the `hex.modsim` file that you have downloaded and click `Open`.

<img width="366" alt="Screenshot 2026-05-17 210855" src="https://github.com/user-attachments/assets/a1b7b6d0-95a4-44ad-ada6-f1eebda3adcc" />
<img width="331" alt="Screenshot 2026-05-17 220958" src="https://github.com/user-attachments/assets/bf5fa7bf-935c-4b11-9177-d9da5c98a263" />

Now you should be able to see the full CPU design and all the components and modules which you can use the controls located at the top left to pause the execution or step through them step-by-step half clock cycle at a time. 

You can see all the available modules that can be used on the left panel and you can hold RMB to move around and use LMB to click and select modules.

### Uploading Custom Instruction Sequence 
As mentioned before, the CPU is connected to a Non-Volatile Memory module that stores instructions and data that is fetched as part of the Fetch instruction cycle. You can upload a special file with an extension `.hex` to the `NRAM` module containing a sequence of 8-bit instrcutions that is included in the `ISA` represented in hexadecimal format seperated by spaces. In the file, you can enter your own custom sequence of instructions you want to be executed by the processor. The memory size is `256 bytes` and each cell is 1 byte a.k.a 1 instruction and operand data. 

> [!IMPORTANT]
> Be careful of how many instructions you enter in the custom file and especially the operand which is the last 4-bit since for WRITE instructions, if the operand happens to be an address which an instruction was placed, it could be overwritten and you will get unexpected results. This is due to both instruction and data being stored in the same memory.
>
> Maybe Harvard Architecture was not that bad eh?

A custom file can be uploaded to the NRAM by clicking the right mouse button on the module and clicking `View/Edit NRAM Data` option. Click `File` on the top left of the NRAM menu and click `Load Data` and select your `custom.hex` file and click open. Now you should see the hex values you wrote in your file in the NRAM cells. Now you can navigate to the module named `CLK` in the timing unit and click the square button reset the simulation and all the values from the modules and click play on the top left to start the simulation of the processor executing your very own custom instruction flow.

As an example of how the custom file should be written, I have uploaded a sample file with 4 instructions that can be found and downloaded called [`mine.hex`](/mine.hex)

## Documentation
An in-depth guide and explanation of the registers, available instructions (ISA) and core components and any other information that is needed to get more grasp of the simulation design can be found [here](/docs/hex.pdf). This document is not mine and is written by `David May` in 2014. All credit goes to the original author.


