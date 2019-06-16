In theory, this should work on Debian, but this has not been tested. Tested on Ubuntu 18.04 bionic.

# Quickstart
`git clone https://github.com/edo9300/ygopro.git edopro`
`cd edopro`
`./install-dependencies-ubuntu.sh`
`./premake5 gmake`
`make -Cbuild`

# Post-build deploy
TODO

# Manually
A good practice is to stay up-to-date! Run `sudo apt-get update && sudo apt-get upgrade`

`premake5` is used to generate makefiles. You can also install it in `/bin` or anywhere in `PATH` instead if you'd like.

List of packages to retrieve from `apt`: `build-essential p7zip-full libevent-dev libfmt-dev libfreetype6-dev libirrlicht-dev liblua5.3-dev libsqlite3-dev libgl1-mesa-dev libglu-dev libcurl4-openssl-dev libgit2-dev libasound2 nlohmann-json3-dev`

`build-essential` is for your GCC C++ compiler and Make.

`libevent-dev libfmt-dev libfreetype6-dev libirrlicht-dev liblua5.3-dev libsqlite3-dev` are YGOPro core dependencies. You can also build and link these yourself if you want to use a newer version than provided by your distro.

`libgl1-mesa-dev libglu-dev` are used on Linux for graphics, i.e. OpenGL.

`libcurl4-openssl-dev libgit2-dev nlohmann-json3-dev` are new dependencies needed by EDOPro. Note that the latest `nlohmann-json3-dev` is only available on the `eoan` Ubuntu repository, so the prebuild script adds that repository temporarily to retrieve it (and then takes it out or we break `apt-get` for other packages). `nlohmann-json-dev` only provides version 2 and we require version 3.

`irrKlang` is also a core dependency but is only available by the download link. To install by hand, you can copy that portion of the script and use your favourite extraction tool (more below). Don't forget to move the `.so` files to the build and deploy directories! `libasound2` is used by irrKlang for some reason (needs confirmation).

Technically, you don't need `p7zip-full`; `unzip` will do, but 7-Zip is far more powerful. For `unzip`, to extract irrKlang, do `unzip -uo irrKlang-64bit-1.6.0.zip` instead.
 
