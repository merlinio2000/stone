(Exceptional Controlflow)

- wait until result is available (io calls)
- current_thread::sleep()
- division by zero


#### Peripheral Registers

![[interr_periph_regs.png]]





# Exceptions on Cortex-M3/M4

Interrupt sources: IRQ0 - IRQ239
- Peripherals signal to CPU about events
- (also doable in software)
- runs async

## System Exceptions

- Reset
	- Restart of processor
- NMI - Non-maskable Interrupt
	- NOT ignorable, e.g. critical hardware error
- Faults
	- undefined instructions, unaligned accesses, etc.
- System Level Calls
	- OS calls - Instruction [[#SVC]] and [[#PendSV]]


![[interr_sys_excp.png]]

#### Interrupt Example

![[interr_exp.png]]







## Vector Table

**"Which [[#ISRs]] should the processor call?"**

![[interr_vector_table.png]]

### ISRs


![[interr_vector_table_addrs.png]]



### Vector Table Initialization

![[interr_vector_table_init.png]]



## Storing the Context

### ISR Call

Interrupt between e.g. TST and BEQ could change the outcome -> processor automatically saves the following onto the stack:
- Status Register xPSR
- Program Counter PC
- LR
- R12
- R0-R3

Stores **EXC_RETURN=0xFFFF_FFF9** into LR to signify that an interrupt handler is currently running -> PC to return is already stored on the stack
### ISR Return

- `BX LR` or  
- `POP {..., PC}`(if LR has been PUSHed in the ISR) or
- Load EXC_RETURN into PC
	- -> restores R0-R3, R12, LR, PC and xPSR
![[interr_isr_ctx_stack.png]]


### Program Status Registers (PSRs)

- APSR [[Arithmetic Operations#APSR (Application Program Status Register)]]
- IPSR Interrupt Program Status Register
- EPSR Execution Program Status Register
- xPSR **combination of all three**

![[PSRs.png]]

![[PSRs_fineprint.png]]



## Interrupt Control

### Nested Vectored Interrupt Controller (NVIC)

![[interr_nested_vec_interr_controller.png]]
### Exception States

(for each interrupt source, e.g. IRQ17)
![[interr_control_excp_state.png]]
![[interr_excp_state_pending.png]]


## Interrupt Masking

PRIMASK
![[interr_primask.png]]



## En-/Disabling  IRQs

![[interr_endisabling_irq.png]]




## Controlling Interrupts from C (CMSIS)

![[interr_cmsis_fns.png]]

### Data Consistency
![[interr_cmsis_data_consistency.png]]

Solution: disable interrupts inside while writing the two bytes to prevent "concurrent" modification
![[interr_cmsis_data_consistency_sol.png]]



# Nested Exceptions (Preemption)

- routine A temporarily interrupts routine B
- each exception assigned a **PRIORITY LEVEL** ([[#Priority Level Registers]])
	- -3 : Reset
	- -2 : NMI
	- -1 : Hard Fault
	- all other priorities programmable
- if priority levels are equal, the **lowest interrupt number determines which runs first**
![[interr_preemption.png]]


### Priority Level Registers

- lower priority level -> greated priority
- 4-bits -> 0\x0 - 0xF

![[interr_prio_level_regs.png]]


#### Nested Priority Example
![[interr_nested_prio_ex.png]]
![[interr_prio_level_ex_hw.png]]



### Special Interrupt Situations

Multiple IRQ Request pulses for the same interrupt, **BEFORE** the ISR enters and is able to handle them, are treated as a **single** input. Individual events are lost
