# Gmod RISC-V Emulator
## Description
The purpose of this project is to fully emulate RV64GC unpivileged ISA and supervisor priviliged ISA. Currently, the emulator can execute RV64I instructions in unprivileged mode. Memory accesses are little-endian.
`ECALL` and `EBREAK` instructions are used to output a0 return value register for now. 
Written in an ingame derivative of Lua called 'E2'.
## Examples
### Fibonacci Numbers
Below is a simple assembly program that outputs Fibonacci numbers indefinitely. First, we assemble it into RISC-V object code.

![image](https://github.com/DanielRottenborn/Gmod-RISCV/assets/48681051/d3a2075d-9160-43dd-b625-e688a7f88a09)

After that, we paste the object code into the emulator. The assembler we used displays object code dump in big-endian format, the program will need to convert it to little-endian format before execution.

![image](https://github.com/DanielRottenborn/Gmod-RISCV/assets/48681051/ca53acf9-1f80-40a2-a922-8ba08e19bd9f)

Finally, as we run the emulator, it outputs the Fibonacci sequence into the console.

![image](https://github.com/DanielRottenborn/Gmod-RISCV/assets/48681051/1b577055-a75b-4623-8f76-6127f060801a)
### Sorting an Array
The C program below sorts an array of 8 elements and then 'prints' out the array. To print out the element, we manually place `ECALL` into print function before returning.
```
int sort(int *data, int count) {
  int i, j, temp;
  for(i = 0; i < count - 1; i++) {  
    for(j = 0; j < count - i - 1; j++){
      if (data[j + 1] < data[j]){
        temp = data[j];
        data[j] = data[j + 1];
        data[j + 1] = temp;
      }
    }
  }
}

#pragma GCC push_options
#pragma GCC optimize ("O0")

int print_element(int *data, int offset) {
  //Manually add ECALL before return
  return data[offset];
}

int main(void) {
  int n[8] = {45, 6, 83, 4, 3, 91, 70, 15};
  sort(n, 8);

  for (int i = 0; i < 8; i++) {
    print_element(n, i);
  }

  return 0;
}

#pragma GCC pop_options
```

_Compilation result_

![image](https://github.com/DanielRottenborn/Gmod-RISCV/assets/48681051/58541d32-7446-4c82-a5f9-6baad6f12a72)

_Emulator output_

![image](https://github.com/DanielRottenborn/Gmod-RISCV/assets/48681051/9c777880-35dd-4cc5-a48e-883eb5e70daf)
