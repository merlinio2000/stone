- function/method/procedure...
- sequnece of instructions to solve subtask
- called by name


### ARM terminology

- Procedure: returns nothing
- Function: returns value
- Routine: in nested contexts
	- caller: a routine
	- callee: subroutine


# Call and Return

![[call_and_return.png]]


## BL \<label>
- unconditional, relative, direct (see [[Branches#Properties]] )
- store current PC in LR
- branch to \<label>
	- PC = PC +/- offset
	- offset range -16'777'216 to 16'777'214

![[bl_instr.png]]

## BLX \<register>
- unconditional absolute indirect
- store current PC in LR
- addr of subroutine in register
- Branch
	- PC = register
	- branch addr from 0 to $2^{32}$

![[blx_instr.png]]



# Nested Subroutines

- remember addresses based on [[Stack]]
- LR gets saved on stack

![[nested_subroutines.png]]


# Instructions using SP

### misc
![[sp_instr.png]]

## Add/Subtract SP (immediate)
- immediate offset \<imm>
- offset range 0-1020d & 0-508d (more than $2^7$ resp $2^8$ bits because only multiples of 4 make sense since SP is word aligned)
![[add_sub_sp.png]]

## Add to SP (register)

![[add_sp_reg.png]]