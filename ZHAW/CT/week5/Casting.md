as always problematic with signed conversions.
E.g. extending $1001b =-7d$ to 8-bits in a naive unsigned way would result in $0000'1001b = 9d$

Beispiel in C

![[C_casting_example.png]]

Explanation of 4th last row: $0111'1111'1111'1111 > 1000'0000'0000'0000$ wich false in unsigned logic



# Extension

```
(S|U)XT(B|H) Rd, Rm ; Extract lowest byte/halfword of Rm and store it
					; into Rd as a 32-bit value
```
## Sign Extension (signed values)

if MSB is $1$ (value is negative) the upper bits will be filled with $1$'s instead of $0$'s

 - SXTB extend 8bit to 32bit value
 - SXTH extend 16bit to 32bit value
 
## Zero Extension (unsigned values)

Fills upper bits with $0$
 - UXTB extend 8bit to 32bit value
 - UXTH extend 16bit to 32bit value



# Truncation

Cut the left most digits

For **signed** this has the risk of changing the sign for a negative value

For **unsigned** this results in a module operation