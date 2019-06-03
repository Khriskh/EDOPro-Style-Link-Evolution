# Windows

## 1) Prerequisites
- Git
- Visual Studio 2015 Update 3 or newer with Visual C++ compilers installed (possible to build with G++, not covered here for now)
- [premake5](https://premake.github.io/download.html)
  - Place it in a folder that's in `PATH`
- [vcpkg](https://github.com/microsoft/vcpkg)
  - Follow the Quick Start instructions after Visual Studio is installed
- OPTIONAL: [DirectX SDK](https://www.microsoft.com/en-us/download/details.aspx?id=6812)
  - If you get [error S1023](https://support.microsoft.com/en-ca/help/2728613/s1023-error-when-you-install-the-directx-sdk-june-2010) when installing this, go to Control Panel > Uninstall a program, uninstall all versions of Visual C++ 2010, and try again

## 2) Clone the repository and submodules
```
git clone https://github.com/edo9300/ygopro.git
cd ygopro
git submodule update --init --recursive
```

## 3) Acquire dependencies
Dependencies are missing from the repository. You could follow the instructions on [Fluorohydride](https://github.com/Fluorohydride/ygopro/wiki/build) but this alternate procedure is easier.

Clone https://github.com/soarqin/ygopro.git and copy the following folders to your edopro repo:
- event
- freetype
- irrlicht
- lua
- sqlite3

Clone https://github.com/fmtlib/fmt.git into `fmt` in your edopro repo.

Download [irrKlang 32-bit](https://www.ambiera.com/irrklang/downloads.html) and extract it to `irrKlang` in your edopro repo.


# Linux

TODO