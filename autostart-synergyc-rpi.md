
## Autostart Synergy Client on Raspberry Pi

Autostart Synergy Client for sharing a keyboard and mouse to the Pi.

Add:
	@synergyc --name raspberrypi <Synergy server address>
	
to one or both of the following:

Apply to current user only:
```
	~/.config/lxsessionLXDE-pi/autostart
```
Apply globally to all users:
```
	/etc/xdg/lxsessionLXDE-pi/autostart
```

Source: http://www.raspberry-projects.com/pi/pi-operating-systems/raspbian/auto-running-programs-gui
