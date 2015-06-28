# Installing on Windows 

Windows takes a bit of extra work. First, download [MSYS2](http://msys2.github.io/) and use the installer. 

Next, from the MSYS2 terminal, install all the required toolchains:

For 32-bit machines:

```sh
$ pacman -S mingw-w64-i686-toolchain
$ pacman -S mingw-w64-i686-cmake
$ pacman -S mingw-w64-i686-boost
$ pacman -S base-devel
```

For 64-bit machines:

```sh
$ pacman -S mingw-w64-x86_64-toolchain
$ pacman -S mingw-w64-x86_64-cmake
$ pacman -S mingw-w64-x86_64-boost
$ pacman -S base-devel
```

Next, download and install LLVM using MSYS2. If the installation directory with CMake is left unchanged, make sure the MSYS2 shell is run as Administrator, as it will install to `C:/Program Files (x86)`. 

```sh
$ mkdir build-llvm && cd build-llvm
$ cmake ../llvm-src -G "MSYS Makefiles"
$ make all install # this will take a while! 
``` 

Finally, you can build and use Orange.

```sh 
$ mkdir build-orange && cd build-orange 
$ cmake ../orange -G "MSYS Makefiles"
$ make all
``` 

Installing to `C:/Program Files (x86)` won't work as `orange.exe` depends on some DLLs from MSYS2 and MINGW. You'll have to run `orange.exe` from inside of the MSYS2 shell. However, any program built using Orange will work outside of the MSYS2 shell. 