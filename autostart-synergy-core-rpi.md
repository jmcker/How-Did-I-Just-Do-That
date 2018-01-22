
## Autostart Synergy Client or Server on Raspberry Pi

Autostart Synergy Client or Server to share a keyboard or mouse between computers.

Add one of the following lines:
#### Client
```
@synergy-core --client --name raspberrypi <Synergy server address>
```
#### Server
```
@synergy-core --server --name raspberrypi -c <path to Synergy config file>
```
to one or both of the following. 

Apply to current user only:
```
~/.config/lxsession/LXDE-pi/autostart
```
Apply globally to all users (Be sure to use `sudo vim autostart` to edit the file or you won't be able to write changes.):
```
/etc/xdg/lxsession/LXDE-pi/autostart
```
The global autostart is overridden if any user autostart that exists in `~/.config`.

4. Write the file and reboot to start Synergy.

Source: http://www.raspberry-projects.com/pi/pi-operating-systems/raspbian/auto-running-programs-gui
