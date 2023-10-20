

# Bitwise Operations


- ANDS -> Bitwise AND `a & b`
- BICS -> Bit Clear `a & ~b`
- EORS -> Exclusive OR `a ^ b`
- MVNS -> Bitwise NOT `~a`
- ORRS -> Bitwise OR `a | b`

![[instr_bitwise_logic.png]]





# Shift / Rotate

- LSLS Logical Shift Left `2^n * Rn` füllt auf mit 0
- LSRS Logical Shift Right `2^{-n} * Rn` füllt auf mit 0
- ASRS Arithmetic Shift Right `2^{-n} * +-A` MSB bleibt MSB  (behält sign)
- RORS Rotate Right LSB wird zu MSB
(rotate left existiert nicht)


![[instr_shift.png]]


### Register Instructions

![[instr_shift_register.png]]
![[instr_shift_imm.png]]