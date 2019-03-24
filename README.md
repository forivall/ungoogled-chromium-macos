# ungoogled-chromium-macos

macOS packaging for [ungoogled-chromium](//github.com/Eloston/ungoogled-chromium).

## Downloads

[Download binaries from the Contributor Binaries website](//ungoogled-software.github.io/ungoogled-chromium-binaries/).

**Source Code**: Use the tags via `git checkout` (see building instructions below). The branches are for development and may not be stable.

## Building

### Software requirements

* macOS 10.12+
* Xcode 8-9
* Homebrew
* Perl (for creating a `.dmg` package)
* Python 2, specifically 2.7.13 or newer, as `python` in PATH
* Python 3.5 or newer as `python3` in PATH

### Setting up the build environment

1. Install Ninja via Homebrew: `brew install ninja`
2. Install GNU coreutils (for `greadlink` in packaging script): `brew install coreutils`
3. Install GNU readline: `brew install readline`
4. Install the data compression tools xz and zlib: `brew install xz zlib`
5. Install Python 3.x: `brew install python`
6. Install Python's pyenv to manage python version: `brew install pyenv`
7. Install Python 2.7.13: `pyenv install 2.7.13`
**Note**: in some cases you might get `Build failed: "ERROR: The Python zlib extension was not compiled. Missing the zlib?"` during Python 2.7.13 installation, this can be fixed by running `CPPFLAGS="-I$(brew --prefix zlib)/include" pyenv install 2.7.13`. 
8. Setup `pyenv`:
```sh
echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bash_profile
```
8. Set global `python` command to use Python 2.7.13: `pyenv global 2.7.13`.
9. Restart your Terminal

### Build

First, ensure the Xcode application is open. Then, run the following:

```sh
git clone --recurse-submodules https://github.com/ungoogled-software/ungoogled-chromium-macos.git
# Replace TAG_OR_BRANCH_HERE with a tag or branch name
git checkout --recurse-submodules TAG_OR_BRANCH_HERE
./build.sh
```

A `.dmg` should appear in `build/`

**NOTE**: If the build fails, you must take additional steps before re-running the build:

* If the build fails while downloading the Chromium source code, it can be fixed by removing `build/downloads_cache` and re-running the build instructions.
* If the build fails at any other point after downloading, it can be fixed by removing `build/src` and re-running the build instructions. This will clear out all the code used by the build, and any files generated by the build.

## Developer info

TODO

## License

See [LICENSE](LICENSE)
