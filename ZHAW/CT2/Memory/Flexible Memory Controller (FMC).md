
Bridges system and external bus for extending on-chip memory, addresses:
- SRAM and NOR flash
- Sync DRAM
- NAND flash


Automatically splits data lines, e.g.:
- write of 32-bits to a bus with only 8 data lines gets translated into
  four writes of 8-bits
- analogous for reads


## Memory Banks

on ST the address range is split into 6 banks, each allows up to 4 connected devices

pins are multiplexed (cant use all at the same time)

![[fmc_memBanks.png]]