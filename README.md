# Overview #

The coredumper library can be compiled into applications to create core dumps of the running program -- without terminating. It supports both single- and multi-threaded core dumps, even if the kernel does not natively support multi-threaded core files.

Coredumper is distributed under the terms of the BSD License.

# Background #

This library is primarily intended to simplify debugging of
long-running services. It is often inacceptable to suspend production
services by attaching a debugger, nor is it possible to crash the
service in order to generate a core file.

By modifying an existing service to take advantage of the coredumper
library, it is possible to expose an interface for obtaining snapshots
of the running application. The library supports writing of core files
to disk (e.g. triggered upon reception of a signal) but it can also
generate in-memory core files.  This makes it possible for web
services to expose remote access to core files.


# Example #

This is by no means a complete example; it simply gives you a feel for what the coredumper API looks like.

```
  #include <google/coredumper.h>
  ...
  WriteCoreDump('core.myprogram');
  /* Keep going, we generated a core file,
   * but we didn't crash.
   */
```

The "examples" directory shows how to add a core file feature to an
existing TFTP server. For an example of how to use on-disk core files,
take a look at "src/coredump_unittest.c".

The code has been tested on Linux x86/32, x86/64, and ARM. It is
distributed from http://code.google.com/p/google-coredumper. It is
available as a tar source archive, and in prebuilt form as Debian and
RedHat packages.


# Build & Install #

For detailed information on how to build and install this library,
read the "INSTALL" file. On most systems, you will need to configure
and build by running:

  ./configure && make

You can then test whether the code works correctly on your system, by
running:

  make check

The check requires that you have access to development tools such as
"readelf", and "gdb".

If you decide to install from the tar file, you now need to run the
following command as "root":

  make install

Alternatively, you can build packages for your targeted distribution
by running either:

  make deb
or
  make rpm

These commands generate installable package files. The packages will
be located in the "packages/<DISTRIBUTION>" directory (e. g. packages/rh9
or packages/woody). The exact path name is printed at the end of the
compilation.

Follow your distribution's instructions on how to install new
packages.

For more information on how to use the library, read the manual pages
for "GetCoreDump" and "WriteCoreDump".
