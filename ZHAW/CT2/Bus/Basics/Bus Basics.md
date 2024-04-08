## Context
#### Timing Diagrams
![[basics_timing.png]]
#### CMOS Inverter
![[basics_cmos.png]]
#### CMOS Tri-State Inverter
![[basics_tri-state-cmos.png]]

Actual Implementation:
![[basics_tri-state-cmos-impl.png]]






# Asynchronous SRAM
![[basics_async_SRAM-read.png]]

- NE, NOE, NWE control the different cycles
- the 'N' prefix (NOE) means a ACTIVE-LOW enable flag

## Read Cycle
![[basics_async_SRAM.png]]

## Write Cycle
![[basics_async_SRAM-write.png]]




# Synchronous Bus

Examples using ST Microelectronics External Bus (see ennis.zhaw.ch)
![[basics_sync_bus.png]]

## Synchronous Write
![[basics_sync_bus_WRITE.png]]


## Synchronous Read
![[basics_sync_bus-READ.png]]



## Bus Access Size
![[basics_sync_bus-access_size.png]]








# Control and Status Registers
![[basics_sync_bus-ControlAndStatus_registers.png]]

![[basics_sync_bus_example.png]]

![[basics_bus_status_regs.png]]













# Address Decoding

How does a slave know that it is the one being addressed?

There is also **partial** decoding, where the decoder ignores parts of the address, useful for group (1:n) addressing

![[basics_bus_address_decoding.png]]






# Dealing with slow slaves

A bus is only as fast as the slowest peripheral attached to it

Depending on the address of the device (known speed) the cpu inserts WAIT states into the read cycle

![[basics_bus_slow_slaves_wait_state.png]]







# Bus Hierarchies

![[basics_bus_hierachies.png]]

