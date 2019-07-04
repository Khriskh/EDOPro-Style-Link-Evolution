Tested on macOS Mojave 10.14.5. A bug with macOS 10.14 prevents graphics from showing up. Binaries are only guaranteed to execute on the version you built on until further notice.

# Quickstart
```bash
git clone https://github.com/edo9300/ygopro.git edopro
cd edopro
git submodule update --init --recursive
./build-support/install-macOS-brew.sh
./build-support/install-macOS-src.sh
./build-support/install-macOS-bin.sh
./premake5 gmake2
make -Cbuild
```
Do `make -Cbuild config=release` to get a release build; otherwise, `debug` is built by default.

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
This packages the executable in the macOS app bundle format with its dylibs and puts everything you need into `deploy/`. Fonts are missing and this will fail to start! Sounds and card scripts are also missing but this is not fatal.
```bash
./build-support/deploy-macOS.sh
```
To deploy a `debug` build, set `BUILD_CONFIG=debug`. Debugging symbols will be stripped from only `release` builds.

# Dependencies (TODO explain them)
## Homebrew (`./build-support/install-macOS-brew.sh`)
Most dependencies are retrieved from [Homebrew](https://brew.sh/). `install-macOS-brew.sh` will automatically set up `brew` if it isn't set up already and install the dependencies. If you prefer to do this yourself, the list of `brew` dependencies is `dylibbundler gpatch p7zip libevent fmt freetype sqlite curl libgit2 nlohmann-json`.

Brew should also automatically install Xcode Command Line Tools. Building with Xcode or GCC is not supported at this time; please use Clang and Make. GCC is symlinked to Clang by default on macOS.

## From source (`./build-support/install-macOS-src.sh`)
By default, `irrlicht` and `lua` are built from source instead of using Homebrew. Sources and buildtrees are downloaded and created in `/tmp`.

`irrlicht` is patched with `irrlicht/irrlicht-macOS.patch`, built with `xcodebuild`, and installed to `/usr/local/include/irrlicht` and `/usr/local/lib/libIrrlicht.a`.

`lua` needs to be built with C++ bindings and the script also takes care of this.

## Binaries (`./build-support/install-macOS-bin.sh`)
<code>[premake5](https://github.com/premake/premake-core/wiki/Using-Premake)</code> is used to generate makefiles. [You can also install it](https://premake.github.io/download.html#v5) in `/usr/local/bin` or anywhere in `PATH` instead if you'd like. If you do this, obviously do `premake5` instead of `./premake5` whereever you see it.

`irrKlang` is also a core dependency but is only available [here](https://www.ambiera.com/irrklang/downloads.html). To install by hand, you can follow that portion of the script.