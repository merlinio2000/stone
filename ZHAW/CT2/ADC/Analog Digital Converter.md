
### Full Scale Range (FSR)

The full scale voltage  $V_{FSR}$ is **one LSB less** than $V_{REF}$

One LSB is worth $V_{REF} / 2^n$

![[adc_fsr_ex.png]]


### How it works

Analog voltage drops over every resistor. 
Individual rest voltages get compared with input voltage
#### Flash ADC

![[adc_howItWorks_flash.png]]


#### Successive Approximation Register (SAR) ADC
Alternative to many comparator ADC [[#How it works]]: 
cheaper implementation "binary searching" for the right voltage
(only one comparator)

![[adc_howItWorks_SAR.png]]











# Sampling Errors

## Quantization Error

Max -0.5 - +0.5 LSB

Can be reduced by increasing bit precison

## Offset Error

![[adc_samplingErr_offset.png]]


## Gain Error

![[adc_samplingErr_gain.png]]




# ADC on STM32F429

- 3 [[#Successive Approximation Register (SAR) ADC]]
- 19 Channels
	- 16 External
	- 3 Internal: V_REF, V_BAT
- each ADC configurable as 12/10/8/6-Bit
	- Left/Right aligned: Result in N most left/right bits (except $N=6$)


### Conversion Modes

![[adc_stm32f429_convModes.png]]


### Timing

![[adc_stm32f429_timing.png]]


##### Conversion Time

$$\Large
T_{total} = T_{sample} + T_{conv}
$$

$T_{sample}$ : programmable for each channel (ADC_SMPR1/2)
$T_{conv}$ : scales with resolution (-> [[#Successive Approximation Register (SAR) ADC]])
	N cycles for N bit resolution




## Watchdog


Allows monitoring the result of a ADC with very little overhead (Interrupt 
triggered when reached)