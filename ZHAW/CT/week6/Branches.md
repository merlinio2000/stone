- **MAY** change PC

### Properties

type:
- conditional, branch only if condition met
- unconditional, always branch

address hand-over:
- direct, target addr part of instruction
- indirect, target addr in reg

address of target:
- relative, target addr relative to PC
- absolute

ARM has **ONLY** these:
- conditional direct relative
- unconditional direct relative & indirect absolute

### Caution: Pipeline and the PC

because of the pipeline which always fetches the next two $16$-bit instructions
the Program Counter PC is always **the current address plus 4**


# Unconditional Branches

## B (direct, relative)

#### Immediate
- relative to PC, 11-bit imm
- -2048d to +2046d, ONLY EVEN NUMBERS
![[B_imm.png]]

![[b_example.png]]

## BX (indirect, absolute)

- Branch and Exchange
![[bx_instr.png]]






# Conditional Branches

## Flag dependent Branches

- **FLAGS** [[Arithmetic Operations#Flags]] must be set from a previous operation (e.g [[#CMP]] or [[#TST]])



![[b_condition_instr.png]]

### Conditions
#### general

|Symbol|Condition|Flag|
|---|---|---|
|EQ   | Equal   | z == 1  |
|NE   | NotEqual  | z == 0  |
|CS   | Carry set  | c == 1 |
|CC   | Carry clear  | c == 0  |
|MI   | Minus/neg  | n == 1  |
|PL   | Plus/pos or zero  | n == 0   |
|VS   | Overflow  | v == 1  |
|VC   | No overflow  | v == 0  |

#### unsigned arithmetic

|Symbol|Condition|Flag|
|---|---|---|
|EQ   | Equal   | z == 1  |
|NE   | NotEqual  | z == 0  |
|HS (=CS) | unsigned higher or same  | c == 1 |
|LO (=CC) | unsigned lower  | c == 0  |
|HI   | unsigned higher | c == 1 and z == 0 |
|LS | unsigned lower or same | c == 0 or z == 1 |

#### signed arithmetic

|Symbol|Condition|Flag|
|---|---|---|
|EQ| Equal   | z == 1  |
|NE| NotEqual  | z == 0  |
|MI| Minus/neg | n == 1 |
|PL| Plus/pos or 0 | n == 0|
|VS| Overflow | v == 1 |
|VC| No overflow| v == 0 |
|GE| Signed >= | n == v |
|LT| Signed < | n != v |
|GT| Signed > | z == 0 and n == v|
|LE| Signed <= | z == 1 or n != v|


## Arithmetic Branches









# Compare and Test

## CMP

- same as **SUBS** from [[Arithmetic Operations#Negative Numbers]]
	- **BUT** doesnt store result
- compare two operands [[#Conditions]]
- **ONLY flags are affected**
- also higher registers

![[cmp_instr.png]]

## CMN

- same as **ADDS** from [[Arithmetic Operations#Addition]] 
	- **but** without storing result
- compare 2 operands **NEGATIVE**
- read as "is content of Rm equal to 2's complement of Rn"
![[cmn_instr.png]]


## TST
- is a specific bit set? **ONLY works for testing ONE bit**
- logical AND [[Logic Instructions#Bitwise Operations]]
	- but without result
![[tst_instr.png]]