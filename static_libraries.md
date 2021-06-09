# Static Libraries

A static library is nothing but a collection of object files. In fact, on
Linux, a static library is often referred to as a static archive and static
library files have the extension `.a`. On linux again, it is created using
the `ar` command as follows:

```
ar -r <archive file name> object_file1 object_file2 ...
```
