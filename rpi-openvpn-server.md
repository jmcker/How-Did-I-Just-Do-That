
## Create an OpenVPN server on a Raspberry PI ##

Using PiVPN.

More detailed information is available on [PiVPN's site](http://www.pivpn.io/) or their [GitHub page](https://github.com/pivpn/pivpn/blob/master/README.md).
This is basically the TL;DR of the TL;DR.

Install:
```
curl -L https://install.pivpn.io | bash
```

Adding clients:
```
pivpn add
# Copy ovpn file to targeted device
# Import into OpenVPN
```

Commands:
```
::: Control all PiVPN specific functions!
:::
::: Usage: pivpn <command> [option]
:::
::: Options:
:::  -a, add [nopass]     Create a client ovpn profile, optional nopass
:::  -c, clients          List any connected clients to the server
:::  -d, debug            Start a debugging session if having trouble
:::  -l, list             List all valid and revoked certificates
:::  -r, revoke           Revoke a client ovpn profile
:::  -h, help             Show this help dialog
:::  -u, uninstall        Uninstall PiVPN from your system!
```

Source: http://www.pivpn.io/
