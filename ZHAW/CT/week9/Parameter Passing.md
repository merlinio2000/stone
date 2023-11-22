
# Passing through Registers

## Pass by Value

![[reg_pass_by_val.png]]

## Pass by Reference

![[reg_pass_by_ref.png]]



# Passing through Global Variables (DONT)

DISCOURAGED

![[pass_by_glob.png]]




















# ARM Procedure Call Standard

AAPCS


Specifies:
![[aapcs_overview.png]]
![[aapcs_dist.png]]


## Register Usage
![[aapcs_reg_usage.png]]


### Scratch Register
- holds intermediate value during a calculation
- usually not named in source code

### Variable Register
- register to hald value of a (routine local) variables
- Cortex-M0: R8-R11 mostly useless because of limited available instructions

### Argument, Parameter
- EQUIVALENT
- formal parameter for a subroutine

### Example
![[aapcs_example.png]]

### In Practice with C

![[aapcs_C.png]]

## Calling Assembly Subroutines from C

![[aapcs_asm_from_C.png]]

## Caller

![[aapcs_caller.png]]


## Callee

![[aapcs_callee.png]]











# Stack Frame

![[stackframe_overview.png]]


## Access to Local Variables

example on word (32bit) sized variables
![[stackframe_locals.png]]

## Stack Frame Example
![[stackframe_ex.png]]