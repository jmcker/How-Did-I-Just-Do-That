
## Physical Boot Switch for Raspberry Pi

Create a physical switch that boots a powered-off Raspberry Pi.


Connect a switch to the GPIO pins: 
	Connect pin 5 (GPIO3) and pin 6 (GND) to the switch (a female jumper cable cut in half and stripped makes this easy).
	On an SPDT switch, pin 6 (GND) would be the common (center) and pin 5 (GPIO3) would be the terminal oppostite the desired throw direction.
```
	  TOP
	[empty]
	[pin 6]			(Switch is thrown to "TOP" to turn "ON")
	[pin 5]
```
	Throwing the switch to "ON" will now boot the Pi when powered off.
	
	Any variety of switch will work. Just wire the terminals for the correct behavior.

Source: https://gilyes.com/pi-shutdown-button/
