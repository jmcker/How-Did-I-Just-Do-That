
## Add entries to the host files on Linux, OSX, and Windows ##

This can be used to resolve names instead of having to remember IPs.

### Windows ###
1. Open the file ```C:\Windows\System32\Drivers\etc\hosts``` as an administrator.
2. Add ip/name pairs:
```
192.168.1.16        therouter
192.168.1.159       mypi
192.168.1.267       someserver
172.221.129.206     externalserver
192.168.1.45:90     internalsite.com
```

### Linux & OSX ###
1. Open the file ```/etc/hosts``` as a super user.
2. Add ip/name pairs (same format):
```
192.168.1.16        therouter
192.168.1.159       mypi
192.168.1.267       someserver
172.221.129.206     externalserver
192.168.1.45:90     internalsite.com
```

Sources:
- https://bencane.com/2013/10/29/managing-dns-locally-with-etchosts/