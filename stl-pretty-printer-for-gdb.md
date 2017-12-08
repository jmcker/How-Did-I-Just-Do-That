
## C++ STL Container Pretty Printer for GDB

Add a Python pretty printer to gdb so that STL containers can be printed nicely.


Checkout (Subversion): 
```
svn co svn://gcc.gnu.org/svn/gcc/trunk/libstdc++-v3/python
```

Add:
```
python
import sys
sys.path.insert(0, '/mnt/d/jmcker/Documents/Git Repos/gdb_printers')
from libstdcxx.v6.printers import register_libstdcxx_printers
register_libstdcxx_printers (None)
end
```
	
to ~/.gdbinit

gdb will display an error message at startup if there is a problem with the path.
It doesn't like tilde expansion, so use a full root path.


Source: https://sourceware.org/gdb/wiki/STLSupport
