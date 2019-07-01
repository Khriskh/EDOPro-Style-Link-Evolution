Tested on Windows 10, Visual Studio 2017 Community and Visual Studio 2019 Enterprise.

# Prerequisites
- [Git Bash](https://git-scm.com/download/win) (this also comes with [GitHub Desktop](https://desktop.github.com/) if you prefer
- [Visual Studio IDE](https://visualstudio.microsoft.com/vs/) 2015 Update 3 or newer, with Visual C++ support installed
- OPTIONAL: DirectX SDK
  - If you get error S1023 when installing this, go to Control Panel > Uninstall a program, uninstall all versions of Visual C++ 2010, and try again
Restart your computer after installing Visual Studio or DirectX SDK.


# vcpkg
Most dependencies for EDOPro will be retrieved from vcpkg. If you prefer to set this up yourself, you can clone it from [here](https://github.com/microsoft/vcpkg). In this case, set `VCPKG_ROOT` to the path you install vcpkg at before running `install-windows-vcpkg.sh`, or install `freetype libevent lua[cpp] sqlite3 fmt curl libgit2 nlohmann-json` for static linking yourself.

# Quickstart
Clone the repository and open a Git Bash terminal there. Run the following
```bash
git submodule update --init --recursive
./build-support/install-windows-bin.sh
./build-support/install-windows-vcpkg.sh
./premake5.exe vs2019 # or your version of Visual Studio
```
*Note*: if you skipped installing DirectX SDK, do `./premake5.exe vs2019 --no-direct3d` instead.
At this point, you can open `build/ygo.sln` and build from the IDE. Alternatively, from the command line, if `msbuild` is in PATH: `msbuild.exe ./build/ygo.sln -m -p:Configuration=Release`

# Post-build deploy
This puts everything you need into `deploy/`. Fonts are missing and this might fail to start! Sounds are also missing but this is not fatal.
```bash
./build-support/deploy-windows.sh 32
```
To deploy a debug build, set `BUILD_CONFIG=debug`

