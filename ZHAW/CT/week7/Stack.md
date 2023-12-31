- **Stack Pointer** SP keeps track of current location on stack
- only push/pop
- starts from stack-base (initial value of SP)
- **ALWAYS** works in WORDs (32-bit) -> SP always WORD aligned
- Stack-Limit < Stack Pointer < Stack-base
- **lowest register stored at lowest address (top of stack)** see [[#Example of storage order]]

### Nested Subroutines

- push current LR (link register) onto stack (M-bit [[#Push]])
- pop LR value back into PC to resume execution at that point ([[#Pop]])

### Implementation

![[stack_impl.png]]

- stack-base is **above** the stack area
	- SP **DECREMENTS** when pushing



# Push

![[stack_push.png]]

- **ONE OR MORE** registered to be stored
- low registers only (reg_list = one bit per reg)
- LR (R14) -> M-bit (no other high reg)
- **lowest register stored at lowest address (top of stack)**
![[stack_push_instr.png]]

![[push_instr_versions.png]]

### Example of storage order

![[push_instr_ex_1.png]]
![[push_instr_ex_2.png]]

# Pop

![[stack_pop.png]]

- **ONE OR MORE** registers to be restored
- low regs only
- PC (R15) -> P-bit (no other high regs)
- lowest register reloaded first
- arguments can be specified as `{R1, R3-R6}` like [[#Push]]
![[pop_instr.png]]



# Operations using SP

- can be used in add/subs like any other register
	- -> SEPARATE OP-CODE
- LDR and STR also like regular
	- -> SEPARATE OP-CODE

![[sp_add_sub.png]]
![[sp_add.png]]
![[sp_ldr_str.png]]