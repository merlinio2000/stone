
only a standard on paper, many different implementations

also called **4-Wire** bus

NO ACK/ERROR detection

## Basics

![[spi_basics_sync.png]]

![[spi_basics_sync_multipleSlaves.png]]


### Implementation using Shift reg

- LSB/MSB configurable on masters, slaves probly hardwired
- [[#Interrrupts]] triggered through TXE/RXNE notify CPU of incoming 

![[spi_basics_impl_shiftReg.png]]

### Timing Diagram

- output toggled on clock edge
- RX samples on other clock edge
- see [[#Modes]]

![[spi_basics_timing.png]]

## Modes

toggle data on one edge, sample on the other
**CPOL** controls this mechanism if the idle level is high(=1) or low(=0)
**CPHA** controls which edge samples/toggles (rising/falling are inverted for idle high - interpret as falling towards idle/rising away from idle)

!!**CPHA=1** causes the signal to be 1/2 clock delayed

![[spi_basics_modes.png]]
![[spi_basics_modes_CPOL-CPHA.png]]

## SPI on STM32F4xxx

NSS = $\overline{SS}$

![[spi_STM32F4_impl.png]]

![[spi_STM32F4_TXE-RXNE.png]]


### Interrrupts

Instead of polling TXE/RXNE the are 2 interrupts SPI1 & SPI2 available

### Registers

SPI_CR1/2 for controlling the SPI
SPI_SR for status bits
SPI_DR contains data received/to transmit  

![[spi_STM32F4_regs.png]]

### Transmitting
![[spi_STM32F4_tx.png]]


### Receiving

![[spi_STM32F4_rx.png]]


### Full-Duplex

![[spi_STM32F4_fullDuplex.png]]





## SPI - Flash Devices

some vendors might also use multiple data lines for faster speeds

![[spi_flash.png]]