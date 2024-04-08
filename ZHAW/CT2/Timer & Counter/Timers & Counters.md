![[timerNcounter.png]]


# Prescaler

Allows to increase counting range.
Count only every $n$-th event e.g. 
- 0b00 -> div by 1
- 0b01 -> div by 2
- 0b10 -> div by 3
- ...


# Counting mode

### Up-counting mode

- counts from $0$ to `ARR` 
- generates counter overflow event



### Down-counting mode

- counts from `ARR` to $0$
- generates counter underflow event

## Center-aligend-counting mode

- count from $0$ to `ARR-1` (!NOTE! $-1$)
- generates counter overflow event
- counts from `ARR` down to $1$
- generates counter underflow event
- restarts from $0$



# Input Capture (CCR)

For measuring intervals / pulse lengths and periods

Per timer there can be multiple `CCR`

Useful for e.g. stop watch
![[timerNcounter_capture.png]]




# Timer Configuration

`RCC` (Reset and Clock Configuration) block must be used to enable on-board timers

Additionally the timer itself gets configured using the `TIMX` block



### Update Event

New configuration for the counter only applies after the **update event (UEV)** was fired.
This event is triggered once the counter register reaches its target
![[timerNCounter_config_uev.png]]



## Clock sources


- internal clock **CK_INT**
- external input pins **TIMx_CH1/2**
- external trigger input **TIMx_ETR**
- internal trigger inputs (**ITRx**)
	(one timer as prescaler for another timer)