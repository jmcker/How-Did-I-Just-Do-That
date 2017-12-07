
## Disable Overscan on Raspberry Pi

Overscan left portions on all four sides of the display unused. Disabling it let the fill the entire screen.


Edit the boot config file with admin privledges: 
	sudo vim /boot/config.txt

Ensure that disable_overscan is uncommented and has a value of 1:
	disable_overscan = 1
	
Reboot to observe the effect.


Source: https://www.raspberrypi.org/forums/viewtopic.php?t=47152
