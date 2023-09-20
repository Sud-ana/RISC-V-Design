# RISC-V-Design
Designing a RISC-V pipeline core 

This git repo demonstates a workflow to design a RISC-V core through ISA. 

# Sections
- [x] Creating and compiling a c-source file into object file
  - [x] Create a source C file
  - [x] Compile it into object file using gcc compiler and interpret the object file
  - [x] Simulate the output to command prompt using spike.
  - [x] Understand program counter and debug register contents using spike debugger.
     


# Creating and compiling a source file into object file
In order to demonstrate the process of high level language interpretation into machine language, we develop a C-source file that is compiled using gcc compiler into object file. The compiler and assembler outputs an object file that has the locations of the registers and the assembly instructions. 

![C-Source code](/assets/Day1_CSourceCode.png)

![C-Source code](/assets/Day1_AssemblerOutput.png)

# Simulate a C program with an assembly function call 
We generate a assembly function in load.S file  and call that function within the C code while compiling using the gcc based riscV compiler 

![C-Source code](/assets/Day2_CCode.png)
![C-Source code](/assets/Day2_AssemblyIncrementCode.png)
![C-Source code](/assets/Day2_SourceAndAssemblyFile.png)

To compile and generate object file I used the following instruction:
  * riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o 1to9_custom.o  1to9_custom.c load.S

Then I simulated the object file through spike with debug option: 
  * Spike pk 1to9_custom.o
    
Finally, I viewed the object file through object dump to interpret the assembly instruction set
  * Riscv64-unknown-elf-objdump -d 1to9_custom.o | less

# Testbench setup to generate the firmware to load onto memory
Now inorder to test the RISC-V core, we create a testbench to load the c code's assembly hex code onto memory. The RISC-V core processor immplemented through a picorv32 RTL reads this hex code and dumps the output into the standard output on the terminal.

![C-Source code](/assets/Day2_collateral_Files_before_running_hex_script.png)

![C-Source code](/assets/Day2_Run_script_to_generate_hex_firmware_for_testbench.png)

![C-Source code](/assets/Day2_Firmware_generated_in_filelist.png)

