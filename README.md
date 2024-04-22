# Gmod RISC-V Emulator
## Description
The purpose of this project is to fully emulate RV64GC unpivileged ISA and supervisor priviliged ISA. Currently, the emulator can execute RV64I instructions in unprivileged mode, operating with little-endian memory.
`ECALL` and `EBREAK` instructions are used to output return value registers for now. 
Written in an ingame derivative of Lua called 'E2'.
## Examples
### Fibonacci Numbers
Below is a simple assembly program that outputs Fibonacci numbers indefinitely. First, we assemble it into RISC-V object code.

![image](https://github.com/DanielRottenborn/Gmod-RISCV/assets/48681051/41ef17be-d0e1-486f-b243-fed3f7c3bb9a)

After that, we paste the object code into the emulator. The assembler we used displays object code dump in big-endian format, the program will need to convert it to little-endian format before execution.

![image](https://github.com/DanielRottenborn/Gmod-RISCV/assets/48681051/3276a6ce-caf1-4d45-bd32-11cb3c99d704)

Finally, as we run the emulator, we can see the Fibonacci sequence in the output.

![image](https://github.com/DanielRottenborn/Gmod-RISCV/assets/48681051/0349ca6f-ba23-4ba4-88e1-4cb9a01e0062)
