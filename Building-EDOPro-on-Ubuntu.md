In theory, this should work on Debian, but this has not been tested. Tested on Ubuntu 18.04 bionic.

# Quickstart
I really hope you have Git.
```bash
git clone https://github.com/edo9300/ygopro.git edopro
cd edopro
git submodule update --init --recursive
./install-dependencies-ubuntu.sh
./premake5 gmake2
make -Cbuild
```

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
TODO

# Manually getting and updating dependencies
A good practice is to stay up-to-date! Run `sudo apt-get update && sudo apt-get upgrade`. This will also ~~hopefully~~ bring your `apt` dependencies up-to-date.

`premake5` is used to generate makefiles. You can also install it in `/usr/local/bin` or anywhere in `PATH` instead if you'd like. If you do this, obviously do `premake5` instead of `./premake5` whereever you see it.

List of packages to retrieve from `apt`: `build-essential p7zip-full libevent-dev libfmt-dev libfreetype6-dev libirrlicht-dev liblua5.3-dev libsqlite3-dev libgl1-mesa-dev libglu-dev libcurl4-openssl-dev libgit2-dev libasound2 nlohmann-json3-dev`

`build-essential` is for your [GCC C++ compiler](https://gcc.gnu.org/) and [Make](https://www.gnu.org/software/make/).

<code>[libevent-dev](https://github.com/libevent/libevent) [libfmt-dev](https://github.com/fmtlib/fmt) [libfreetype6-dev](https://www.freetype.org/index.html) [libirrlicht-dev](http://irrlicht.sourceforge.net/) [liblua5.3-dev](https://www.lua.org/download.html) [libsqlite3-dev](https://www.sqlite.org/index.html)</code> are YGOPro core dependencies. You can also build and link these yourself if you want to use a newer version than provided by your distro.

<code>[libgl1-mesa-dev](https://www.mesa3d.org/) [libglu-dev](https://www.opengl.org/resources/libraries/)</code> are used on Linux for graphics, i.e. OpenGL.

<code>[libcurl4-openssl-dev](https://github.com/curl/curl) [libgit2-dev](https://github.com/libgit2/libgit2) [nlohmann-json3-dev](https://github.com/nlohmann/json)</code> are new dependencies needed by EDOPro. Note that the latest `nlohmann-json3-dev` is only available on the [eoan Ubuntu repository](https://packages.ubuntu.com/search?keywords=nlohmann-json3-dev), so the prebuild script adds that repository temporarily to retrieve it (and then takes it out or we break `apt-get` for other packages). `nlohmann-json-dev` [only provides version 2](https://packages.ubuntu.com/search?keywords=nlohmann-json-dev) and we require version 3.

`irrKlang` is also a core dependency but is only available [here](https://www.ambiera.com/irrklang/downloads.html). To install by hand, you can copy that portion of the script and use your favourite extraction tool (more below). Don't forget to move the `.so` files to the build and deploy directories! `libasound2` is used by irrKlang for some reason (needs confirmation).

Technically, you don't need `p7zip-full`; `unzip` will do, but [7-Zip](https://www.7-zip.org/) is far more powerful. For `unzip`, to extract irrKlang, do `unzip -uo irrKlang-64bit-1.6.0.zip` instead.
 

