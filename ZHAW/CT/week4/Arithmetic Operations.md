**specifically** for Cortex-M0

## Negative Numbers

In twos complement
Unsigned:
$$
b_3 * 2^3 + ... + b_0 * 2^0
$$
Signed:
$$
\textcolor{red}{-b_3} * 2^3 + ... + b_0 * 2^0
$$

![[signed_unsigned.png]]



### Twos Complement (TC)

How do I get from $a$ to $-a$

$$
\begin{align}
a - a = 0 \leftrightarrow & a + inv(a) + 1 = 0 \\
& -a = inv(a) + 1 = TC(a) 
\end{align}
$$
-> Inverting then $+1$


In the [[#ALU]] this can be done like this:

![[tc_alu_impl.png]]

#### RSBS (TC instruction)
- calculates the [[#Twos Complement (TC)]] of $Rn$ into $Rd$
- updates flags
- only low reg

![[rsbs_instr.png]]
































# ALU

Arithmetic Logic Unit, contains full-adders etc to carry out math instructions

ALU does **NOT** know whether its working with unsigned (Cout) or signed (V) -> C & V are always calculated ([[#APSR (Application Prgram Status Register)]])

![[CT/week4/alu_overview.png]]
![[alu_overview 1.png]]

## Flags

- Carry = wrapping from unsigned $1111$ to $0000$
- Overflow = wrapping from signed $0111$ (7) to $1000$ (-8) 

### APSR (Application Program Status Register)


![[apsr_flag.png]]
- **MRS** move reg from special reg
- **MSR** move to special reg from reg
Using **32-bit OPCODE**

![[apsr_instrs.png]]




# Addition

Summary:
- ADDS with flag update
- ADD without
![[add_instr_summary.png]]


### ADDS (with flag update)
- only low register

![[adds.png]]


#### ADDS (immediate) - T1
- two low regs
- imm value $[0,7]$
![[adds_imm_1_instr.png]]

#### ADDS (immediate) - T2
- **Rdn** is both result and operand (low reg)
- imm value $[0,255]$

![[adds_imm_2_instr.png]]

### ADD (NO flag update)
- high or low register
- **Rdn** is both result and operand
![[add_instr.png]]









## Carry vs Overflow

also see [[#APSR (Application Program Status Register)]]

![[carry_overflow_add.png]]

![[carry_overflow_add2.png]]
