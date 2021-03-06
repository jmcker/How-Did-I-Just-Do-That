
## Synergy Server Configuration

Create a custom configuration for Synergy. Manually adds the RPi as a client and sets up hotkeys for screen swapping.

1. Create the file *synergy.sgc* using any text editor.
2. Add all screens to the screens sections like below:
```
section: screens
	JMCKER-NEWPC:
	raspberrypi:
	raspberrypi-250:
end
```
3. Link the screens in the desired configuration:
```
section: links
	JMCKER-NEWPC:
		right = raspberrypi
	raspberrypi:
		left = JMCKER-NEWPC
		right = raspberrypi-250
	raspberrypi-250:
		left = raspberrypi
end
```
These could also optionally be linked on both sides (useful later):
```
section: links
	JMCKER-NEWPC:
		left = raspberrypi
		right = raspberrypi
	raspberrypi:
		left = JMCKER-NEWPC
		right = raspberrypi-250
	raspberrypi-250:
		left = raspberrypi
		right = JMCKER-NEWPC
end
```
Visually, this would look something like:
```
<Screen 1><Screen 2><Screen 3><Screen 1>
````

4. Customize the options section with the desired options:
```
section: options
	relativeMouseMoves = false
	screenSaverSync = true
	win32KeepForeground = false
	clipboardSharing = true
	switchCorners = none 
	switchCornerSize = 0
	keystroke(Alt+Tilde) = switchInDirection(right)
	keystroke(Alt+Shift+Tilde) = switchInDirection(left)
end
```

The full list of options and explanations can be found [here](https://github.com/symless/synergy-core/wiki/Text-Config#options).

### Swap Keys
The keystroke command can be used to add a shortcut for swapping screens.
```
keystroke(Alt+Tilde) = switchInDirection(right)
```
If the screens are linked on both sides as part four mentioned, only one key is needed to cycle through all screens.
If this is not the case, however, another key is needed to go the opposite direction. In the above example, this is:
```
keystroke(Alt+Shift+Tilde) = switchInDirection(left)
```
A list of keys and commands other than swapping is available [here](https://github.com/symless/synergy-core/wiki/Text-Config#Keynames).

### Loading the Configuration File
#### GUI
From the server dialog, choose *synergy.sgc* as an existing configuration file and start the server.
#### Command Line
Start `synergy-core --server` with the `-c` option followed by the path to the configuration file.
```
synergy-core --server -c ~/synergy.sgc
```
To debug any problems with the configuration file or connections, launch the server in the foreground with the `-f` option.
```
synergy-core --server -f -c ~/synergy.sgc
```



Source: 
- https://github.com/symless/synergy-core/wiki/Text-Config
- https://davejamesmiller.wordpress.com/2013/02/23/synergy-hotkey-to-toggle-screens/
- https://github.com/symless/synergy-core/wiki/Command-Line#synergys-options

Complete example: [.synergy.conf](https://github.com/jmcker/.cfg/blob/master/.synergy.conf)
