Tested on macOS Mojave 10.14.5. A bug with macOS 10.14 prevents graphics from showing up. Binaries are only guaranteed to execute on the version you built on until further notice.

# Homebrew
Most dependencies are retrieved from [Homebrew](https://brew.sh/). `install-macOS-brew.sh` will automatically set up `brew` if it isn't set up already and install the dependencies. If you prefer to do this yourself, the list of `brew` dependencies is `dylibbundler p7zip libevent fmt freetype irrlicht sqlite curl libgit2 nlohmann-json`.

Brew should also automatically install Xcode Command Line Tools. Building with Xcode or GCC is not supported at this time; please use Clang. GCC is symlinked to Clang by default on macOS.

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
This packages the executable in the macOS app bundle format with its dylibs and puts everything you need into `deploy/`. Fonts are missing and this will fail to start! Sounds are also missing but this is not fatal.
```bash
./build-support/deploy-macOS.sh
```
To deploy a `debug` build, set `BUILD_CONFIG=debug`. Debugging symbols will be stripped from only `release` builds.