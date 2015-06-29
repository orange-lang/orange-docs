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

Now, you can build and use Orange. 

```sh 
$ git submodule init && git submodule update 
$ mkdir build-orange && cd build-orange 
$ cmake ../orange -G "MSYS Makefiles"
$ make all
``` 

Note that if you wish to install Orange and the dependencies it built (like LLVM), you will have to run MSYS2 as an Administrator as the default installation location is C:/Program Files (x86) on 64-bit machines. You can customize the installation path to avoid this. 

However, using Orange installed to `C:/Program Files (x86)` won't work as `orange.exe` depends on some DLLs from MSYS2 and MINGW. You'll have to run `orange.exe` from inside of the MSYS2 shell. Regardless of this, any program built using Orange will work outside of the MSYS2 shell. 