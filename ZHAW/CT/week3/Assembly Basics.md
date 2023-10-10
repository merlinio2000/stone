### C example
NOTE: compiler does not use [[#Pseudo Instruction]] in this case, see 3)
![[c_example.png]]





# Loading Data

![[registers.png]]



## Register to Register

### `MOV/MOVS <Rd> <Rm>`

copy value from **REGISTER** `Rm` to **REGISTER** `Rd`
- mov works for low and high regs
- movs works ONLY for low regs

![[mov_movs.png]]



# Literal to Register


### MOVS immediate

![[movs_imm.png]]



### EQU
![[equ.png]]




### Load - `LDR` (literal)

![[load_ldr.png]]
![[ldr_example.png]]





## Pseudo Instruction

[[#Load - `LDR` (literal)]]] is a pseudo instruction, literal value gets stored in the [[#Literal Pool]]
![[ldr_pseudo.png]]
![[pseudo_example.png]]




## Literal Pool
Convenient localtion in the code segment where the assembler allocates and initializes memory. Used by e.g. [[#Load - `LDR` (literal)]]








