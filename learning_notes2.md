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
4. `beq x3, x0, +16`
	1. Fetch
		1. CPU fetches instruction from next ram address, as explained in previous steps.
	2. Decode
		1. The instruction is decoded as `beq x3, x0, +16`. Which will result in a comparison of values stored in register addresses x3 and x0. If equal, the pc will go to pc + specified imm value (16) instead of the default +4.
		2. ![image](https://github.com/user-attachments/assets/aedeb002-2798-41bc-8e0c-a8638e7e58e8)

	3. ALU
		1. The ALU starts by calculating the current PC address of 0000000c plus the immediate value (16: represented as 00000010 in base-16), obtaining the memory address to be accessed in the PC if the comparison is equal.
		2. ![image](https://github.com/user-attachments/assets/caa4a7ff-f70d-4163-a74d-8e20a4128ad6)

	4. Compare
		1. The comparator is passed the data held in specified register addresses x3 (represented in cell a) and x0 (cell b). The result (in this step) is false, resulting in the PC progressing as usual.
		2. ![image](https://github.com/user-attachments/assets/d1220870-8ead-4896-9ab7-81e564bb0d1d)

	5. Mem/Reg
	6. PC
		1. As stated above, due to a `false` result, PC moves as usual.
		2. ![image](https://github.com/user-attachments/assets/61bcc91f-a79f-4f2c-b1dd-bfcc5e6eabe5)

5. `sb x3, 0(x2)`
	1. Fetch
		1. Processed as in previous steps.
		2. ![image](https://github.com/user-attachments/assets/3d382c6f-be52-4a26-ab83-23a568dd79c5)

	2. Decode
		1. `sb x3, 0(x2)` function is decoded. This will instruct the CPU to transfer data held in some specified register (x3)  to be stored in a computed memory address (immediate value 00000000 + data stored in register x2 )
		2. ![image](https://github.com/user-attachments/assets/74fd19cc-177c-4b6e-91ff-ba9eb26d7536)

	3. ALU
		4. The ALU loads an addition operation to add the immediate (in cell b) to the data retrieved from register address x2 (held in cell a). The result is then used as the memory address to store data held in register x3
		5. ![image](https://github.com/user-attachments/assets/b88f4fd6-b0c8-483b-90c7-4649f300a4b9)

	4. Compare
	5. Mem/Reg
		1. In this step, the program comes alive. We can see that the computed memory address c0000000 corresponds to the Text I/O address, and the data passed from register x3 (00000048) corresponds to the character "H" in this text I/O.
		2. ![image](https://github.com/user-attachments/assets/e8508fa2-b7aa-4c22-be37-b14836b7d887)

	6. PC
		1. Increments as usual.
6. `addi x1, x1, 1`
	1. Fetch
		1. Performed as previously described.
	2. Decode
		1. The instruction is described as the familiar addi function, adding data held in register x1 with imm value 00000001 and storing the result in rs1. It is easy to tell that this specific instruction serves as the counter increment for the loop that is ran to print Hello.
		2. ![image](https://github.com/user-attachments/assets/2ed59be9-d098-4135-b006-ce84adbe82c8)

	3. ALU
		1. x20 is pulled from register x1, adding imm value of x1, we get 33 as our result, or x21 as denoted in base-16. 
		2. ![image](https://github.com/user-attachments/assets/38df5d08-30c6-43ff-8c99-24dda2434f8c)

	4. Compare
	5. Mem/Reg
		1. ALU resultant is stored in specified register x1.
		2. ![image](https://github.com/user-attachments/assets/2cee8f69-1fde-430b-8cbd-d1700ebda447)

	6. PC
		1. Increments as usual.
7. `jal x0, -16`
	1. Fetch
		1. Fetches as previously described, normal increment.
	2. Decode
		1. In this instruction, we receive the jal function in the form of `jal x0, -16`. This function is telling us to store the next pc address (current +4) in register address x0 and to then jump to memory address current + imm value (-16, noted as fffffff0 to subtract using base 16)
		2. ![image](https://github.com/user-attachments/assets/1821ffae-5c8a-46c7-a9f9-757dce5c5f1f)

	3. ALU
		1. The ALU adds current PC (x18) to fffffff0 (think of it as ffffffff - 16, or max value minus 16) to obtain x18 minus 16, resulting in x8 (remember, subtracting 16 from 18 in base 16).
		2. ![image](https://github.com/user-attachments/assets/7966263e-c0cc-453c-885a-f9274e8b862c)

	4. Compare
	5. Mem/Reg
	6. PC
		1. The PC now goes back to address x8, bringing us to the 3rd instruction in our original instruction set. 
		2. ![image](https://github.com/user-attachments/assets/8bf56716-4db3-4cb2-8bcc-24c8e9aa7b3a)

8. Running the loop until `jal x0, 0` (stored in x1c)
	1. The program now goes back to our third instruction. This loop will continue to run in order to print our entire desired string into the text I/O. 
	2.![image](https://github.com/user-attachments/assets/bd54d016-7c04-4e40-8c63-bb1a61814f2c)

	3. Dfe
9. D
10. D
