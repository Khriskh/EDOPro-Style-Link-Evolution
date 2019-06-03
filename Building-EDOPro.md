# Windows

## 1) Prerequisites
- Git
- Visual Studio 2015 Update 3 or newer with Visual C++ compilers installed 
  - Possible to build with G++, not covered here for now
- [premake5](https://premake.github.io/download.html)
  - Place it in a folder that's in `PATH`
- [vcpkg](https://github.com/microsoft/vcpkg)
  - Follow the Quick Start instructions after Visual Studio is installed
- OPTIONAL: [DirectX SDK](https://www.microsoft.com/en-us/download/details.aspx?id=6812)
  - If you get [error S1023](https://support.microsoft.com/en-ca/help/2728613/s1023-error-when-you-install-the-directx-sdk-june-2010) when installing this, go to Control Panel > Uninstall a program, uninstall all versions of Visual C++ 2010, and try again

Make sure you restart your computer after you install these.

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

With `vcpkg` install additional dependencies:
```
PS> .\vcpkg install libgit2 curl nlohmann-json
```

## 4) Create the project files

If you're not building with DirectX, add `no-direct3d` to `premake5.lua` as a parameter (@edo9300 how?)

Run the following commands from the command line in the `ygopro` folder.

` premake5 gmake ` if you're not using Visual Studio

` premake5 vs* ` (with the current edition of Visual Studio installed on your system)
there are also premake4 scripts that are synced with the premake5 ones to use on systems where premake5 isn't availabe, or just as preference, but note that with visual studio builds, the max edition supported by those scripts is 2010.

This generates `*.sln` and `*.vcxproj` files into `build`. Open `ygo.sln` in Visual Studio.

## 5) Correct typos

Expand the `ygopro` project in Solution Explorer and delete `ygopro.rc`. This is a resource file that generates icons for the executable.

If you're building with DirectX, the SDK may not have been added to the include paths. (It should be; I probably forgot to reboot, so feel free to try without this step.) To rectify, right-click on `irrlicht` in Solution Explorer and choose Properties. Go to `C/C++` and add `C:\Program Files (x86)\Microsoft DirectX SDK (June 2010)\Include` or where your SDK got installed to Additional Include Directories

`irrlicht` has a typo in a code file. Open the project and find `src\CD3D9ShaderMaterialRenderer.cpp`. Replace all instances of `LoadLibraryA` with `LoadLibrary` in the file.

## 6) Build

Well, after navigating through this hell for hours, you are finally ready to build EDOPro. Build the entire solution in Visual Studio ~and come cry to us on Discord when it inevitably fails somewhere~

OLD notes: If you are on windows using Visual Studio, and you used premake4, first right click on ygopro in the solution explorer, and then set it as startup project. To build with Visual Studio click on build->build solution, or click local windows debugger that will first compile the program then launch it. On other systems, go with the terminal in the build folder, then run make config=release to build the static program.

## 7) Running your build

Crying yet after the number of hours as there are steps in this? Behold the wonder of open source!

The executable is located in `bin\debug` unless you picked to build differently, in which case it'll be in a different subfolder. To keep things tidy, we'll copy or move the important stuff out of this folder.

Make a new folder elsewhere and put all the `*.dll`s and `ygopro.exe` into it. Also copy `irrKlang\bin\win32-visualStudio\irrKlang.dll` into this new folder. At this point, this should be your folder:
- ygopro.exe
- git2.dll
- irrKlang.dll
- libcurl-d.dll
- zlibd1.dll

*You still can't start yet.* You'll need some supporting resources. You can copy these from an existing or fresh Percy installation or similar (I think we have a repo somewhere?). 
- cards.cdb
- strings.conf
- system.conf
- fonts\
- textures\

## 8) Actually running your build

Bless! Double-click `ygopro.exe` and pray. If it errors, check `error.log` and ~complain to us on Discord~.


# Linux

TODO