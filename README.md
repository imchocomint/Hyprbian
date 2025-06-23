# Hyprbian
The ultimate guide to install lastest Hyprland on Debian sid/trixie/experimental (since Hyprland package for Debian is super outdated)

# NOTE: Won't work on Debian 12 or lower. Untested on Ubuntu, but it should work.

# NOTE 2: Things may break. Please don't ask me for help (unless for compiling stuffs).

# NOTE 3: Thank you guys at the JaKoolIt Discord server for promoting and testing my project

## Prerequisites
- A brain to read the official documentations
- Debian ~~13 (trixie)/~~ sid/experimental
- Some libraries; we'll cover them later
- Experience with make, cmake and the like
- make, cmake, clang
- Patience and time (3+ hours) (and maybe a good CPU)
- sway or KDE to install, as well as copy and pasting code

## Installing Hyprland (as a dummy package)
If you're on sid, run ` sudo apt install hyprland `. It will install Hyprland (0.41).

And if you are on Trixie and didn't have the chance to install [before Debian mod team removed the packages](https://tracker.debian.org/news/1648117/hyprland-removed-from-testing/), you're free to download [their .deb packages from Debian web site](https://packages.debian.org/sid/amd64/hyprland/download), or see [Optimization techniques](https://github.com/imchocomint/Hyprbian/blob/main/optimization-technique.md) to learn how to stay on Trixie while still using sid packages.

### Partial explanation
Since the base-files package (defines Debian version) version is shared between testing (13;trixie) and sid, Debian mistook all sid installation to be trixie, therefore not allowing user to install hyprland and its dependencies. This would be resolved when trixie is separated from unstable later this year.

## Installing required libraries & dependencies (yet to be completed)
Please do all of these steps in their correct order. Do not skip any step or do something you are not supposed to at the time. I can't guarantee success if you decide not to obey.
### Installing system dependencies (first)
Install libgbm-dev libre2-dev libxcb-icccm4-dev libxcb-res0-dev libxcb-errors-dev libtomlplusplus-dev. All of which are available in trixie/sid repository.
### Downloading packaged development libraries (second)
Download all .deb packages and install them from [Releases](https://github.com/imchocomint/Hyprbian/releases). 

This will be updated twice a month. Credits to PikaOS team.

### Install aquamarine and hyprutils from the debs (third)
Install hyprutils, libhyprutils and libhyprutils-dev from the .deb files first.

Install aquamarine from the .deb file.

### Install other libraries from the debs (fourth)
Install libhyprcursor, libhyprlang-dev, libhyprlang and libhyprcursor-dev from the .debs file.

Install the rest of the packages from the .deb files.

### Compile and install the remaining dependencies (fifth)
The remaining Hypr* dependencies are:
- hyprlang
- hyprcursor
- hyprgraphics

I would recommend a tool called Pacstall. It do work in most cases, but have some errors (will be discussed later).

You should compiles the binaries as their guide (on GitHub), and manually install them on top of older version installed via apt.


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
Dependencies are all above
```
git clone --recursive https://github.com/hyprwm/Hyprland
cd Hyprland
make all && sudo make install
```
You can recompile the software to update it, I guess.

### Via Pacstall
` pacstall -I hyprland `

If it do require compiling xdg-desktop-portal-hyprland, audit the build file. Change "debian:sid" to "debian:trixie" since Pacstall mistakes sid as Trixie (see above to know why)

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
