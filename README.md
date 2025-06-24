# Hyprbian-guix
The ultimate guide to install lastest Hyprland on Debian sid/trixie/experimental (since Hyprland package for Debian is super outdated) via GNU Guix

# Please do not trust this for now. I need a tester.

# NOTE: Won't work on Debian 12 or lower. Untested on Ubuntu, but it should work.

# NOTE 2: Things may break. Please don't ask me for help (unless for compiling stuffs).


## Prerequisites
- A brain to read the official documentations
- Debian 13 (trixie)/sid/experimental
- GNU Guix
- make, cmake, clang
- Patience and time (3+ hours) (and maybe a good CPU)
- sway or KDE to install, as well as copy and pasting code


## Installing required libraries & dependencies (to be added)

## Install GCC 15 (not applicable to experimental)
Unless you want to update, do not run this script on Debian experimental as it comes with GCC 15 (as well as libstdc++15) on default

Adapted from [this guide](https://medium.com/@xersendo/moving-to-c-26-how-to-build-and-set-up-gcc-15-1-on-ubuntu-f52cc9173fa0)

### Required softwares
` sudo apt install -y build-essential git make gawk flex bison libgmp-dev libmpfr-dev libmpc-dev python3 binutils perl libisl-dev libzstd-dev tar gzip bzip2 `

### Build steps (and install)
```
export CONFIG_SHELL=/bin/bash
mkdir ~/gcc-15
cd ~/gcc-15
git clone https://gcc.gnu.org/git/gcc.git gcc-15-source
cd gcc-15-source
git checkout releases/gcc-15.1.0 # Lastest, for now
./contrib/download_prerequisites
cd ~/gcc-15
mkdir gcc-15-build
cd gcc-15-build
../gcc-15-source/configure --prefix=/opt/gcc-15 --disable-multilib --enable-languages=c,c++
make -j$(nproc)
sudo make install
sudo update-alternatives --install /usr/bin/gcc gcc /opt/gcc-15/bin/gcc 100
sudo update-alternatives --install /usr/bin/g++ g++ /opt/gcc-15/bin/g++ 100
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-14 50
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-14 50
```
then remove the entire source folder

To change between GCC versions:
```
sudo update-alternatives --config gcc
sudo update-alternatives --config g++
```

## Install libstdc++15
Script created by Gemini Pro (with human QA). Battle-tested by at least 3 instances.
### Required softwares
` sudo apt install build-essential gawk bison flex texinfo libgmp-dev libmpfr-dev libmpc-dev `
### Build steps (and install)
```
wget https://ftp.gnu.org/gnu/gcc/gcc-15.1.0/gcc-15.1.0.tar.xz
tar -xf gcc-15.1.0.tar.xz
cd gcc-15.1.0
./contrib/download_prerequisites
mkdir build
cd build
../configure --prefix=/opt/gcc-15 --enable-languages=c,c++ --disable-multilib
make -j$(nproc) all-gcc
make -j$(nproc) all-target-libgcc
make -j$(nproc) all-target-libstdc++-v3
sudo make install-target-libstdc++-v3
echo "/opt/gcc-15/lib64" | sudo tee /etc/ld.so.conf.d/gcc-15.conf
sudo ldconfig
sudo ldconfig -p | grep libstdc++.so
```
then remove the entire folder.

It should work. Had to thank Google for that.

## Install Hyprland
tba


## QnA
### Is it safe?
Ans: If it isn't, I wouldn't have typed this.
### [Should I really trust an AI](https://www.reddit.com/r/debian/comments/1lg5yyo/comment/mzajhgg/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)
I knew it! Someone has already asked this question.

I have a neutral attitude about GenAI in general. I do not always trust them, but use them to tackle challenges in domains which I don't know anything about.

Rest assured, this script is battle-tested, and do work in at least 3 differrent instances. And multiple people QA'd this.

Maybe though. If you don't like it, get out or create a pull request with something safer.
### My compile time is so high
Ans: Same brother, same. It took me an afternoon to compile GCC 15, and an evening to compile libstdc++15 on an i5-1135G7.
### Can we update to newer version?
Ans: Until hyprland change their dependencies, just compile the newer version and reinstall Hyprland.
### Why not nix (package manager)?
Ans: Can't (really) forward that to SDDM.
### Why not Guix?
Ans: This seems like a good idea. I will test it. But maybe it still requires libstdc++15 after all.
### Why not (any other distro)?
Ans: Some people have programs that works only on Debian (hell, what kind of monster would make that?) or is actively working on Debian compatability or is developing Debian, and they can't switch.

# 
So yeah. This may be the end. Thank you for reading all of this. Make sure to star this repo and share if you love it.
