# Learning Notes for emulsiV
**Link title:** emulsiV  
**URL:** https://eseo-tech.github.io/emulsiV/

## Explaining "Hello" Example

### Instructions
During the course of the Hello program, multiple assembly functions are called to execute the CPU instructions. In describing how the function works, the below list of functions will be referenced. Each function is given a description followed by the format of its syntax.
1. **addi**: Adds value from specified register address (rs1) to some specified immediate value (imm) and then stores it in the specified register address (rd)
	`ADDI rd, rs1, imm`
2. **lui**: Loads specified value (imm) into specified register address (rd)
	`LUI rd, imm`
3. **lbu**: Adds some immediate value (imm) to the value stored at the specified registry address (rs1) then looks up that summed value in the memory address and stored the data from that address into the specified register location (rd)
	`LBU rd, imm(rs1)`
4. **beq**: Evaluated if the values stored in register addresses rs1 and rs2 are equal. If true, the program counter shifts to current counter value (pc) to pc + some specified value (imm), else the program continues with its default pc+4 next instruction. 
	`BEQ rs1, rs2, imm`
5. **sb**: Stores the data held in a specified memory address (rs2) in the memory address computed by adding some specified value (imm) to the data held in a specified register address (rs1)
	`SB rs2, imm(rs1)`
6. **jal**: Stores the next address to be accessed from program counter (pc +4) in the specified register (rd), then moves the program counter to the current address plus some specified value (imm) 
	`JAL rd, imm`

Variable Reference:
- imm = immediate value. Some specified data, as opposed to an address to access.
- rd = the address in the register that is being accessed for use in the specified function; specifically the destination where output will be loaded. 
- rs = the address in the register that is being accessed for use in the specified function; specifically the address where data is extracted for use by the function.
### Program Steps
Below is a description for the steps carried out for the given initial values held in the memory. Each step will describe how the CPU processes the instructions.

![image](https://github.com/user-attachments/assets/64280926-0ffd-459c-9026-f9ea5cf2e575)

1. `addi x1, x0, 32`
	1. Fetch
		1. When the CPU starts, it's program counter initiates a fetch at memory address 0000000 via sending a signal to pull that addresses' data via the bus. That data is then passed into the instruction register to be decoded. 
		2. ![image](https://github.com/user-attachments/assets/562e946c-b186-4438-9282-d9755acc5099)


	2. Decode
		1. The data *02000093* is decoded as a function of addi (see above table for function descriptions), with an rs1 of 0, an rd of 1, and an imm value of 00000020. The function will tell the ALU that it must perform an addition as its arithmetic operation, and signal that is must add the imm value (00000020) to the data held in register at addres rs1 (0), then store that at address rd (1).
		2. ![image](https://github.com/user-attachments/assets/ccb1c088-8f6e-4f41-a936-8fb7fb272055)


	3. ALU
		1. The ALU loads its required data based on the decoded instruction described above: loading data from x0 into operand A, immediate value of 00000020 into operand B and then outputting the resultant of the operation (00000020) into r.
		2. ![image](https://github.com/user-attachments/assets/0733cf39-c82b-44c1-a3bf-f8b083d4583b)


	4. Mem/Reg
		1. The ALU stores data r into the specified register address from the decoded instruction (x1) above.
		2. ![image](https://github.com/user-attachments/assets/d5e3a505-9f82-4312-887b-fddb2a8dad2d)

	5. PC
		1. The program counter performs it's default increment (+00000004), indicating the next memory address to be fetched. 
		2. ![image](https://github.com/user-attachments/assets/365e3056-cc7e-46ff-883a-f396c9f20e2e)

2. D
3. D
4. D
5. D
6. D
7. D
8. D
9. D
10. D
