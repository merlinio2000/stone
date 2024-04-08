
designed as an $n \times m$ matrix
- $n$ = number of word lines
- $m$ = number of bit lines

![[mem_design.png]]

# Non-Volatile Memory

## PROM - Programmable Read Only Memory

Programmable, **but only once**
- apply high voltage to transitors(cells) that should be high($=1$) to fuse them during "programming"

![[mem_prom_transistorFuse.png]]

## EEPROM - Electronically Erasable PROM

Reprogrammable version of [[#PROM - Programmable Read Only Memory]]

Individual cells can be reprogrammed using **'Floating Gate' Transistors**

Negative: High cell area -> low densisty (high cost per bit)

Set cell to '$0$' -> ON
	deposit high voltage charge on floating gate
		(isolated bi SiO2)
Erase cell to '$1$' -> OFF
	 discharge floating gate
	 transistor is now off


![[mem_eeprom_floatingGate.png]]

## Flash

simlar to [[#EEPROM - Electronically Erasable PROM]]
but: 
- smaller area -> cheaper cost per bit
- Negative: erasing can only be done in blocks


### NOR vs NAND Topology

![[mem_flash_norVsNandTopo.png]]






# Volatile Memory


## SRAM - Static Random Access Memory

cells based on flip-flops (latches)

- all access take about the same time
- access time independent of location in memory and previous accesses
- no refresh required

![[mem_sram_design.png]]
![[mem_sram_designCell.png]]



### Asynchronous SRAM

![[mem_asyncSram_design.png]]





## SDRAM - Synchronous Dynamic RAM

Information stored as charge in capacitor.

**NEEDS REFRESH**
- capacitors leak current
- to prevent this the charge gets refreshed periodically
	- this is where the 'dynamic' in the name comes from

Addressing:
- both row & column address required
- here each cell contains 8 bit, not just one

![[mem_sdram_design.png]]


- VERY efficient for sequential column access (row address can stay constant)

![[mem_sdram_seqAcccess.png]]




## SRAM vs SDRAM
![[mem_sramVsSdram.png]]