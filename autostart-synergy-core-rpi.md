
## Autostart Synergy Client or Server on Raspberry Pi

Autostart Synergy Client or Server to share a keyboard or mouse between computers.

### On PIXEL:
1. From the Pi Preferences menu, select Default Applications for LXSession.
2. Select the Autostart tab.
3. Add one of the following lines:
#### Client
```
@synergy-core --client --name raspberrypi <Synergy server address>
```
#### Server
```
@synergy-core --server --name raspberrypi -c <path to Synergy config file>
```
See [this page](https://github.com/jmcker/How-Did-I-Just-Do-That/blob/master/synergy-server-configuration.md) for instructions on creating the Synergy config file.

4. Confirm and reboot to start Synergy.



### On LXDE:
Add one of the following lines:
#### Client
```
@synergy-core --client --name raspberrypi <Synergy server address>
```
#### Server
```
@synergy-core --server --name raspberrypi -c <path to Synergy config file>
```
to one or both of the following. (Be sure to use `sudo vim autostart` to edit the file or you won't be able to write changes.)

Apply to current user only:
```
~/.config/lxsession/LXDE-pi/autostart
```
Apply globally to all users:
```
/etc/xdg/lxsession/LXDE-pi/autostart
```

Source: http://www.raspberry-projects.com/pi/pi-operating-systems/raspbian/auto-running-programs-gui
