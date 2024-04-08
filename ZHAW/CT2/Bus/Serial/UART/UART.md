
! Frequencies of sender and receiver may not match exactly
![[bus_uart_freq_mismatch.png]]


**CLOCK Synchronization** happens using start and stop bits, the receiver uses the first few data packets to find a clock that matches the expected pattern -> incurrs overhead

LSB FIRST

# Timing

Enables tolerance of 0.5 Bit / Packet since sampling occurs in the middle of each clock tick
![[bus_uart_timing.png]]


### Timing Settings
![[bus_uart_timing_settings.png]]




# UART Protocols
## RS-232

Rated up to 10 meters
Logic '1' -> \[-3V, -15V\]
Logic '0' -> \[3V, 15V\]

![[bus_uart_rs232.png]]


## RS-485

Uses differential signals -> less susceptible to disturbances / longer distances
Capacitive coupled noise affects both lines -> gets canceled out to a large extent

![[bus_uart_rs485.png]]






# U(S)ART on STM32F4xxx

![[bus_uart_stm32f4_overview.png]]


### Registers
![[bus_uart_registers.png]]