# Installing on Windows

Windows takes a bit of extra work. You'll need to download and install the following:
  - [MinGW-builds](http://mingw-w64.org/doku.php/download/mingw-builds)
    - When installing, set threading model to be `win32`
    - When installing, set exception handling to be `seh`
  - [CMake](http://www.cmake.org/download/)
    - When installing, add CMake to the system PATH.
  - [Python](https://www.python.org/downloads)

This document will take you through the process of downloading Orange. It
assumes that you have git downloaded and installed from
[here](https://msysgit.github.io), with "Use Git from the Windows Command
Prompt" set.

Open your installation of MinGW-builds. By default, it would have installed to
`C:\Program Files\mingw-w64\x86_64-5.1.0-win32-seh-rt_v4-rev0` if you are running
a 64-bit system.

Inside of the MinGW shell, navigate to the directory where you want to download
Orange.

Finally, run these commands:

```sh
$ git clone https://github.com/orange-lang/orange.git
$ cd orange
$ git submodule init
$ git submodule update
$ mkdir build-orange
$ cd build-orange
$ cmake .. -G "MinGW Makefiles"
$ mingw32-make
```

That last command can take a _long_ time, so go grab a drink!

## Building Native Binaries

If you wish to build native binaries, you'll have to first add MinGW to your
system PATH. Extend your system path to include
`C:\Program Files\mingw-w64\x86_64-5.1.0-win32-seh-rt_v4-rev0\mingw64\bin`.

Next, you'll need to install Orange. Open a MinGW shell as Administrator and
navigate back to the directory where you downloaded orange. Then, run these
commands:

```sh
$ cd orange/build-orange
$ mingw32-make install
```

This will install Orange and some dependencies to `C:\Program Files (x86)\orange`.
However, note that the installed `orange.exe` won't work unless it's running
through the MinGW shell, as it depends on some DLLS provided from it.
