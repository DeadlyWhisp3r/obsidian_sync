
2026-02-22 18:05

Tags: [[RISC-V]]

# Riscv Instruction Set
The risc-v is built upon shorter, simpler instructions here a few of those will be explained and the syntax for the assembly code can be seen.

````r
ld x1,45(x2)
#load x1 with the memory from address x2+45 offset
add rd, rs1, rs2
#add rs1 + rs2 in rd
sub rd, rs1, rs2
#sub rd = rs1 - rs2
`````

### Instruction formats
R-type
Instruction format 

| Instruction format | Primary use                           | rd                                 | rs1                                       | rs2                                | Imm                              |
| ------------------ | ------------------------------------- | ---------------------------------- | ----------------------------------------- | ---------------------------------- | -------------------------------- |
| R-type             | Register- register ALU inst.          | Destination                        | First source                              | Second source                      | -                                |
| I-type             | ALU immediates Load                   | Destination                        | First source base regsiter                | -                                  | Value displacement               |
| S-type             | Store Compare and branch              | -                                  | Base register first source                | Data source to store second source | Displacement offset              |
| U-type             | Jump and link, Jump and link register | Register destination for return PC | Target address for jump and link register | -                                  | Target address for jump and link |
|                    |                                       |                                    |                                           |                                    |                                  |
The different instruction formats are encoded in the op-code and decide how the instructions look
![[Pasted image 20260222204334.png]] 
These are how the different instructions look for different instruction formats/types. Page 26 in reference [1]

![[Pasted image 20260222204103.png]] 
![[Pasted image 20260222204127.png]] Page 609-610 in reference [1]

### Clustered OP-codes
Older CISC istruction sets have unique op-codes for each instruction, ADD, SUB, OR, etc. While RISC tells what type of instruction it is and therefore what it should do.

### Funct3 and Funct7 fields
The funct3 field it used by the ALU to determine what kind of operation it is, ADD/SUB, OR, AND, Shift-left, etc. The funct7 field is used to distinguish between ADD/SUB because they share the same funct3 field aswell as opcode.

A interesting observation is that SUB exists but not SUBI. This is because the immediate is already sign extended and you know if you want to add +5 or -5 however for a register you do not know what value is stored in for example x3 and therefore you would have to convert it to a negative value, which you do for non immediates.

### rs1, rs2 and rd fields
Because the fields rs1, rs2 and rd are always in the same place that makes decoding easier.
# References
https://docs.riscv.org/reference/isa/_attachments/riscv-unprivileged.pdf [1]