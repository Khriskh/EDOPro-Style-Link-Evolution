In theory, this should work on Debian, but this has not been tested. Tested on Ubuntu 16.04 Xenial and 18.04 Bionic. You may not need to build dependencies from source on newer distros.

# Quickstart
I really hope you have Git and `curl`. If you don't know what `apt` is either, this guide is not for you.
```bash
git clone https://github.com/edo9300/ygopro.git edopro
cd edopro
git submodule update --init --recursive
./build-support/install-ubuntu-apt.sh
./build-support/install-ubuntu-src.sh
./build-support/install-ubuntu-bin.sh
./premake5 gmake2
make -Cbuild
```
Enter your password for `sudo` when prompted.

# Rebuilding
```bash
make -Cbuild clean
rm -rf build
git pull
git submodule update --init --recursive
./premake5 gmake2
make -Cbuild
```

# Post-build deploy
This strips debugging symbols from only `release` and puts everything you need into `deploy/`. Fonts are missing!
```bash
./build-support/deploy-ubuntu.sh
```
To deploy a `debug` build, set `BUILD_CONFIG=debug`. Debugging symbols will not be stripped.

# Manually getting and updating dependencies
A good practice is to stay up-to-date! Run `sudo apt-get update && sudo apt-get upgrade`. This will also ~~hopefully~~ bring your `apt` dependencies up-to-date.

All `./build-support` scripts must be run from our repository root.

## From `apt` (./build-support/install-ubuntu-apt.sh)
List of packages to retrieve from `apt`: `build-essential cmake curl p7zip-full libevent-dev libfmt-dev libfreetype6-dev libirrlicht-dev liblua5.3-dev libsqlite3-dev libgl1-mesa-dev libglu-dev libgit2-dev libasound2 nlohmann-json3-dev`

`build-essential` is for your [GCC C++ compiler](https://gcc.gnu.org/) and [Make](https://www.gnu.org/software/make/). <code>[cmake](https://cmake.org/)</code> generates Makefiles for the libraries that we're building from source, similar to Premake. `curl` is a command-line utility that retrieves files from the internet and doesn't always come preinstalled. (Could also use `wget`.)

Technically, you don't need `p7zip-full`; `unzip` will do, but [7-Zip](https://www.7-zip.org/) is far more powerful. If using `unzip`, do `unzip -uo <zip_file>` instead.

<code>[libevent-dev](https://github.com/libevent/libevent) [libfreetype6-dev](https://www.freetype.org/index.html) [libirrlicht-dev](http://irrlicht.sourceforge.net/) [liblua5.3-dev](https://www.lua.org/download.html) [libsqlite3-dev](https://www.sqlite.org/index.html)</code> are YGOPro core dependencies. You can also build and link these yourself if you want to use a newer version than provided by your distro.

<code>[libgl1-mesa-dev](https://www.mesa3d.org/) [libglu-dev](https://www.opengl.org/resources/libraries/)</code> are used on Linux for graphics, i.e. OpenGL.

<code>[libgit2-dev](https://github.com/libgit2/libgit2) [nlohmann-json3-dev](https://github.com/nlohmann/json)</code> are new dependencies needed by EDOPro. 
<code>[libcurl4-dev](https://github.com/curl/curl)</code> is also a new dependency but `libcurl4-gnutls-dev` is installed already by `libgit2-dev`.

## From source (./build-support/install-ubuntu-src.sh)
<code>[fmt](https://github.com/fmtlib/fmt)</code> is a YGOPro core dependency. Unfortunately, `libfmt-dev` is not available on Xenial and is only version 4 on Bionic, so we will build against the latest source version. If this ever becomes unstable, we will specify a stable commit/release on GitHub.

<code>[nlohmann-json](https://github.com/nlohmann/json)</code> is a new dependency. Unfortunately, `nlohmann-json3-dev` and `nlohmann-json-dev` are not up to date or available for Xenial and Bionic, so we will again build against the latest source version.

## Binaries (./build-support/install-ubuntu-bin.sh)
<code>[premake5](https://github.com/premake/premake-core/wiki/Using-Premake)</code> is used to generate makefiles. [You can also install it](https://premake.github.io/download.html#v5) in `/usr/local/bin` or anywhere in `PATH` instead if you'd like. If you do this, obviously do `premake5` instead of `./premake5` whereever you see it.

`irrKlang` is also a core dependency but is only available [here](https://www.ambiera.com/irrklang/downloads.html). To install by hand, you can copy that portion of the script and use your favourite extraction tool (more below). Don't forget to move the `.so` files to the build and deploy directories! (You can also move it to the system libraries folder.) `libasound2` is also used by irrKlang and doesn't always come installed, so make sure you get it from `apt`.

 

