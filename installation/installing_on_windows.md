# Installing on Windows

Windows takes a bit of extra work. You'll need to download and install the following:
  - MinGW-w64
	- [64-bit](http://downloads.sourceforge.net/mingw-w64/x86_64-5.1.0-release-posix-seh-rt_v4-rev0.7z)
	- [32-bit](http://downloads.sourceforge.net/mingw-w64/i686-5.1.0-release-posix-dwarf-rt_v4-rev0.7z)
  - LLVM
	- [64-bit](https://github.com/rfratto/llvm/releases/download/v3.6.2/llvm-win-mingw64-posix-seh.zip)
	- [32-bit](https://github.com/rfratto/llvm/releases/download/v3.6.2/llvm-win-mingw32-posix-dwarf.zip)
  - [CMake](http://www.cmake.org/download/)
    - When installing, add CMake to the system PATH.

This document will take you through the process of downloading Orange. It
assumes that you have git downloaded and installed from
[here](https://msysgit.github.io), with "Use Git from the Windows Command
Prompt" set.

1. Download & extract MinGW-w64 to a location of your choice (`C:\` is recommended)
2. Download & extract LLVM to the same location as MinGW-w64 (if you extracted MinGW-w64 to `C:\`, extract LLVM to `C:\mingw64`)
3. Add `C:\mingw64\`bin to your system path
  - Open explorer
  - Right-click My Computer/This PC
  - Select 'Properties'
  - Select 'Advanced system settings' from the left-hand column
  - Select the 'Advanced' tab
  - Select 'Environment Variables'
  - Under 'System Variables', scroll down to the 'Path' item
  - Select the 'Path' item and click 'Edit'
  - Append the system path with `;` and then the `bin` folder of mingw64
  	- In our example, one would append `;C:\mingw64\bin`
  - Press 'OK' on both dialogs to save your changes.
4. From the Windows command prompt (`cmd` from the Start Menu):
  - Run `gcc --version`. Ensure that some version of gcc is installed (this should work as MinGW-w64 includes it)
  - Run `llvm-config --version`. Ensure that this command returns `3.6.2`. 
5. From the command prompt, run these commands:

```sh
$ git clone https://github.com/orange-lang/orange.git
$ cd orange
$ mkdir build
$ cd build
$ cmake .. -G "MinGW Makefiles" -DCMAKE_INSTALL_PREFIX="[Your MinGW-w64 path, e.g. C:\mingw64]"
$ mingw32-make all install
$ orange --help # this is just to ensure it installed
```