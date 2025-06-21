# Hyprbian
The ultimate guide to install lastest Hyprland on Debian sid/trixie/experimental (since Hyprland package for Debian is super outdated)

# NOTE: Won't work on Debian 12 or lower. Untested on Ubuntu, but it should work.

## NOTE 2: Things may break. Please don't ask me for help (unless for compiling stuffs).

## Prerequisites
- A brain to read the official documentations
- Debian 13 (trixie)/sid/experimental
- Some libraries; we'll cover them later
- Experience with make, cmake and the like
- make, cmake, clang
- Patience and time (3+ hours) (and maybe a good CPU)
- sway or KDE to install, as well as copy and pasting code

## Installing required libraries & dependencies (TBA)
Listed dependencies are:
- aquamarine
- hyprlang
- hyprcursor
- hyprutils
- hyprgraphics
- hyprwayland-scanner
- xdg-desktop-portal-hyprland

as well as their libraries (except the last one). Some should be on GNU Guix (although I recommend against this method). Pacstall have all of these, but you should not expect this too much. Safest way is to build their binaries, then find a way to copy the files manually.

Alternatively you can use a Debian source that have all of these softwares and libraries prepackaged. PikaOS' repository is a good choice.

You also need tomlplusplus and its development libraries. This is hidden from the official documentations.

If you're on APT, use this to install libraries: ` sudo apt install lib<softwarename>-deb `. Replace <softwarename> with what you need.

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
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-13 50
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-13 50
```
then remove the entire source folder

To change between GCC versions:
```
sudo update-alternatives --config gcc
sudo update-alternatives --config g++
```

## Install libstdc++15
Script created by Gemini Pro. I used this on my main machine, so no need to worry.
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

## QnA
### Is it safe?
Ans: If it isn't, I wouldn't have typed this.
### Should I really trust an AI
Ans: Fuck off, or read all of the above again.
### My compile time is so high
Ans: Same brother, same. It took me an afternoon to compile GCC 15, and an evening to compile libstdc++15 on an i5-1135G7.
### Can we update to newer version?
Ans: Until hyprland change their dependencies, just compile the newer version and reinstall Hyprland.
### How do we install hypr dependencies
Ans: Right now I can't give you a detailed guide, but the easiest way is to clone their GitHub repository and compile them.
### Isn't compiling everything the purpose of Gentoo?
Ans: I just love Debian. Thank you.
### Why not (any other distro)?
Ans: Above.


# 
So yeah. This may be the end. Thank you for reading all of this. Make sure to star this repo and share if you love it.
