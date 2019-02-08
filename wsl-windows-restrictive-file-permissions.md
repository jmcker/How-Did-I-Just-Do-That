
## UNIX File Permissions on Windows Subsystem for Linux

Mitigate file permission issues (and increase security) when using programs that require restrictive file permissions.
Examples include: Git's credential caching feature, SSH agent, GnuPG, etc.

### Background ###
With WSL (Windows Subsystem Linux), I prefer to do most of my work and keep most of my files and folders outside of the normal WSL Linux root.
Working in the normal Windows filesystem allows me to share and work on files with both graphical Windows and CLI WSL tools.
The default ```HOME``` directory for WSL is ```/home/$USER```, but because of my workflow, I opted to change mine to my Windows home directory at ```/mnt/c/Users/me``` (aka ```C:\Users\me```).
The choice to do this came with a couple caveats.

Since WSL does not support Linux filesystem permissions on NTFS, everything gets 777 permission (read, write, and execute privileges for all).
This causes issues with programs that check for excessive file permissions as a security precaution, including Git's credential caching mechanism and ssh's keystore.
Since WSL abides by real permissions on the Linux side of the filesystem, however, the problem can be fixed via symbolic linking.

By creating a folder with the correct permissions in the original WSL home (```/home/$USER```) and symlinking it into the Windows home (```/mnt/c/Users/me```), the issue is resolved.
WSL sees a properly permissioned folder still under the ```$HOME``` directory.

The only downside is that you lose access to the folder on the Windows side of things.
Since Windows can't understand the symlink, the file that appears is useless.
I typically just right click go to the ```General``` tab and check ```Hidden``` to hide the file.

### Git ###

In the case of Git's ```.git-credential-cache```:

```bash
# Move the existing folder or create a new one
mv /mnt/c/Users/$USER/.git-credential-cache /home/$USER/.git-credential-cache || mkdir /home/$USER/.git-credential-cache

# Assign the proper permissions to the folder
chmod 700 /home/$USER/.git-credential-cache

# Create the soft link
ln -s /home/$USER/.git-credential-cache /mnt/c/Users/$USER/.git-credential-cache
```


### SSH ###

SSH's ```.ssh``` folder becomes a problem if you use SSH keys:

```bash
# Move the existing folder or create a new one
mv /mnt/c/Users/$USER/.ssh /home/$USER/.ssh || mkdir /home/$USER/.ssh

# Assign the proper permissions to the folder
chmod 740 /home/$USER/.ssh

# Create the soft link
ln -s /home/$USER/.ssh /mnt/c/Users/$USER/.ssh
```

### GnuPG ###

```bash
# Move the existing folder or create a new one
mv /mnt/c/Users/$USER/.gnupg /home/$USER/.gnupg || mkdir /home/$USER/.gnupg

# Assign the proper permissions to the folder
chmod 700 /home/$USER/.gnupg

# Create the soft link
ln -s /home/$USER/.gnupg /mnt/c/Users/$USER/.gnupg
```

### Generalization ###
The general move and symlink strategy can really be applied to any program.

Sources:
- https://wpdev.uservoice.com/forums/266908-command-prompt-console-windows-subsystem-for-l/suggestions/13309479-emulate-posix-compliant-filesystem-permissions