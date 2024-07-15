# Learning Notes for emulsiV
**Link title:** emulsiV  
**URL:** https://eseo-tech.github.io/emulsiV/

## Explaining "Hello" Example

### Instructions
1. **addi**: Adds value from specified register address (rs1) to some specified immediate value (imm) and then stores it in the specified register address (rd)
	ADDI rd, rs1, imm
2. **lui**: Loads specified value (imm) into specified register address (rd)
	LUI rd, imm
3. **lbu**: Adds some immediate value (imm) to the value stored at the specified registry address (rs1) then looks up that summed value in the memory address and stored the data from that address into the specified register location (rd)
	LBU rd, imm(rs1)
4. **beq**: Evaluated if the values stored in register addresses rs1 and rs2 are equal. If true, the program counter shifts to current counter value (pc) to pc + some specified value (imm), else the program continues with its default pc+4 next instruction. 
	BEQ rs1, rs2, imm
5. **sb**: Stores the data held in a specified memory address (rs2) in the memory address computed by adding some specified value (imm) to the data held in a specified register address (rs1)
	SB rs2, imm(rs1)
6. **jal**: Stores the next address in program counter (pc +4) in the specified register (rd), then moves the program counter to the current addres plus some specified value (imm) 
	JAL rd, imm
