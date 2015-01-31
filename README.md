# Instructions for installing Haskell

[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/pittsburgh-haskell/haskell-installation?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

These instructions are for GHC 7.8.4, and will be kept up to date to the latest released version of GHC.

## Why does this set of instructions exist?

Why this set of instructions about how to install Haskell on your computer? Isn't the official site for [Haskell](http://haskell.org/) sufficient?

Sadly, right now (January 2015), the answer is *no*, for unfortunate reasons that newcomers should not have had to deal with when getting started. The Haskell community is working to improve the setup process, with a [brand new Web site that has not officially launched yet](http://new-www.haskell.org/), but the information there is not entirely up to date either, although the [download page](http://new-www.haskell.org/downloads) is getting there.

I have personally created Haskell setups on Mac OS X, Windows, and Linux (Ubuntu), and have created the following instructions for these platforms.

## Understanding the fully set up environment

Before following the instructions below, it may be helpful to first understand, at a high level, the end goal of the installation process:

- Install the right version of [GHC](http://www.haskell.org/ghc/), the *de facto* standard native compiler and interpreter.
- Install the right version of [Cabal](http://www.haskell.org/cabal/), the building/packaging tool. Cabal is implemented in Haskell.
- Initialize use of Cabal, letting it create a directory `.cabal` in your home directory and download the list of packages from [Hackage](http://hackage.haskell.org/), the standard Haskell community package archive.
- Install, using Cabal, some auxiliary tools, Happy and Alex, which are needed for Cabal to build and install some packages.

## Instructions

### Mac OS X

Although it is possible to use a [ZIP archive](http://new-www.haskell.org/downloads/osx) of GHC 7.8.3, I recommend using [Homebrew](http://brew.sh/) if on a Mac post-Lion, in order to get GHC 7.8.4. Do

```console
brew install ghc
brew install cabal-install
cabal update
cabal install alex happy
```

Then, in your shell startup file, add `$HOME/.cabal/bin` to your `PATH`, e.g., in my `$HOME/.zshrc` I have

```sh
export PATH="$HOME/.cabal/bin:$PATH"
```

Restart your terminal and you're ready to go.

### Windows

A Windows installer is available at [minghc](https://github.com/fpco/minghc).

There are 32-bit and 64-bit installers, e.g., for the latest 64-bit version, download and run the installer for [GHC 7.8.4, 64-bit](https://s3.amazonaws.com/download.fpcomplete.com/minghc/minghc-7.8.4-x86_64.exe). This installer also includes pre-built Alex and Happy, so all you have to do is go to a command window and do

```console
cabal update
```

### Linux

Full Linux instructions are [here](http://new-www.haskell.org/downloads/linux). Currently, the instructions are for GHC 7.8.3, but 7.8.4 has been out.

For Ubuntu, for example, do

```console
sudo apt-get update
sudo apt-get install -y software-properties-common
sudo add-apt-repository -y ppa:hvr/ghc
sudo apt-get update
sudo apt-get install -y cabal-install-1.22 ghc-7.8.4
cat >> ~/.bashrc <<EOF
export PATH=~/.cabal/bin:/opt/cabal/1.22/bin:/opt/ghc/7.8.4/bin:$PATH
EOF
export PATH=~/.cabal/bin:/opt/cabal/1.22/bin:/opt/ghc/7.8.4/bin:$PATH
cabal update
cabal install alex happy
```

## Final required step: testing your installation

Since we want to be writing and running tests immediately ("test-driven learning"?), we want to install `doctest`, `hspec`, and `quickcheck`. One great way to do this and verify that your installation is working is to try to run a successful build and test of an excellent starter Haskell project, [`unit-test-example`](https://github.com/kazu-yamamoto/unit-test-example):

```console
git clone https://github.com/kazu-yamamoto/unit-test-example
cd unit-test-example
cabal install --enable-tests --only-dependencies
cabal configure --enable-tests
cabal build
cabal test
```

Note that the `cabal install` command will install the dependencies found in the `unit-test-example.cabal` file. **Ideally, you should run this before the workshop, to save on a flood of WiFi access on site to pull down and build dependencies there.**

Your setup is complete for the workshop when `cabal test` succeeds.

If you want to jump ahead before the workshop, you can look at an explanation of what this process does, in the provided [tutorial](https://github.com/kazu-yamamoto/unit-test-example/blob/master/markdown/en/tutorial.md).

## Questions?

If you have any questions or corrections, please open a GitHub issue or submit a pull request!
