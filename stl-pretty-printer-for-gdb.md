
## C++ STL Container Pretty Printer for GDB

Add a Python pretty printer to gdb so that STL containers can be printed nicely.


Checkout the required repo (Subversion) into $HOME/bin/:
```
svn co svn://gcc.gnu.org/svn/gcc/trunk/libstdc++-v3/python
```

Add:
```
python
import sys
import os
sys.path.insert(0, os.path.expandvars('$HOME/bin/gdb_printers'))
from libstdcxx.v6.printers import register_libstdcxx_printers
register_libstdcxx_printers (None)
end
```
	
to ~/.gdbinit

gdb will display an error message at startup if there is a problem with the path.


Source: 
- https://sourceware.org/gdb/wiki/STLSupport
- https://docs.python.org/2/library/os.path.html#os.path.expandvars
