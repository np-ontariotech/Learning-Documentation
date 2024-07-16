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

2. `lui x2, 0xc0000`
	1. Fetch
		1. The CPU accesses the new memory address from the PC, loading in the new address and data into the bus and passing the data into the instruction register to be decoded.
		2. ![image](https://github.com/user-attachments/assets/70d4620f-31bd-41c1-9f0d-22494b48f315)

	2. Decode
		1. LUI function of `lui 2, c0000000` is loaded, which will load the imm value to specified register at address 2. 
		2. ![image](https://github.com/user-attachments/assets/7b64edf7-16a9-4078-9f76-fe262a43e931)

	3. ALU
		1. ALU specifies operation 'b', meaning resultant will just be value in b. This resultant will be passed on to register.
		2. ![image](https://github.com/user-attachments/assets/c33f1190-3a92-4005-aa13-6c726811d0f8)

	4. Mem/Reg
		1. Resultant from the ALU is stored in the register specified in original instruction in the instruction register.
		2. ![image](https://github.com/user-attachments/assets/fc4d36e3-3937-48f1-9ffd-6efdf4d05bea)

	5. PC
		1. As in previous step, the default program counter increment is added to access the next instruction.
		2. ![image](https://github.com/user-attachments/assets/d475bcd6-96e3-4b40-8cd3-ec1c462e0a14)

3. `lbu x3, 0(x1)`
	1. Fetch
		1. CPU fetches instruction from next ram address, as explained in previous steps.
		2. ![image](https://github.com/user-attachments/assets/980c036e-48a4-43de-963f-a26213d65b43)

	2. Decode
		1. LBU function of `lbu x3, 0(x1)` is decoded. Indicating it will access the value held in register x1, add the immediate value of 00000000 to the data held in x1, then extract the data held at the memory address of that summed value, and finally load that data into register x3.
		2. ![image](https://github.com/user-attachments/assets/5a736172-f0a9-4ade-b77c-ae84e719ae70)

	3. ALU
		1. As described above, data in x1 is added to imm to obtain memory address to be accessed. 
		2. ![image](https://github.com/user-attachments/assets/0c4c9a47-2810-4060-9778-1c7bd8619429)

	4. Mem/Reg
		1. Memory address r (from ALU) is accessed. Data held in that address, specifically unsigned byte for the lbu function, is then accessed into the bus and then stored into previously specified memory address x3
		2. ![image](https://github.com/user-attachments/assets/6d4eff7e-465b-431b-a6c5-89f678166515)

	5. PC
		1. Default instruction memory step is performed, exactly as described above.
3. D
4. D
5. D
6. D
7. D
8. D
9. D
10. D
