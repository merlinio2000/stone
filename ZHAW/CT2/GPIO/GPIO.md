Based on the STM F4 Datasheet/Reference Manual

![[gpio_pin_sharing.png]]

![[gpio_rep_slave_sync_bus.png]]

# GPIO Structure

Hardware structure of a single bit in a 16-bit GPIO port (e.g. D.7)
This one pin can have multiple functions (in, out, alternate, analog) functions depending on the mode

![[gpio_structure_hardware.png]]


# Configuration

### Direction

#### mode register (GPIOx_MODER)

MODER\[1:0]:
- 00 Input
- 01 General Purpose output mode
- 10 Alternate function mode
- 11 Analog Mode

![[gpio_config_modeRegs.png]]


### Output Type
#### output type register (GPIOx_OTYPER)

OTYPER:
- 0 Output push-pull
- 1 Output open-drain
![[gpio_otypeReg_push-pull_open-drain.png]]


##### Open drain
![[gpio_config_open-drain.png]]

open drain **with** Pull-Up resistor
![[gpio_config_open-drain_pullUp.png]]


### Pull-Up/Pull-Down

#### Pull-up/Pull-down register (GPIOx_PUPDR)

PUPDR\[1:0]:
- 00 No pull-up / no pull-down
- 01 Pull-up
- 10 Pull-down
- 11 Reserved



### Speed

#### Output speed register (GPIOx_OSPEEDR)

OSPEEDR\[1:0]:
- 00 Low speed
- 01 Medium speed
- 10 High speed
- 11 Very High speed



## I/O Ports

#### Port input data register (GPIOx_IDR)

Set the pin x to read-only

#### Port output data register (GPIOx_ODR)

Set the pin x to read-write


## Setting and clearing bits

#### Port bit set/reset register (GPIOx_BSRR)
![[gpio_config_bitSetResetReg.png]]



## Cookbook

- Find pin number related to GPIOx or vice versa
- Configure using the registers under [[#Configuration]]
- Configure for the correct data operations 
	- Input [[#Port input data register (GPIOx_IDR)]]
	- Output [[#Port output data register (GPIOx_ODR)]]
		or [[#Port bit set/reset register (GPIOx_BSRR)]]






# Hardware Abstraction Layer (HAL)

![[gpio_hal_C_example.png]]