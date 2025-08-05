# Painless Hyprbian
The ultimate guide to install lastest Hyprland on Debian sid/trixie/experimental (since Hyprland package for Debian is super outdated), using dark magic.

# NOTE: Won't work on Debian 12 or lower.

# NOTE 2: Please consider carefully before following this guide. You're going to make your system a [FrankenDebian](https://wiki.debian.org/SourcesList#Precautions).


## Prerequisites
- A brain to read the official documentations
- Courage
- Debian [trixie](https://media.discordapp.net/attachments/1400812641034960977/1402077346084950188/image.png?ex=689299c8&is=68914848&hm=374c06c9efacbb167d7cfce31022d6de76ee64f4d12daba8559f22c55897b8dc&=&format=webp&quality=lossless&width=921&height=516)/sid/experimental
- make, cmake, clang
- sway or KDE to install, as well as copy and pasting code

## Adding experimental repo
```
sudo touch /etc/apt/sources.list.d/experimental.sources
sudo nano /etc/apt/sources.list.d/experimental.sources
```

Inside the file, paste this:
```
Types: deb deb-src
URIs: http://deb.debian.org/debian/
Suites: experimental
Components: main contrib non-free non-free-firmware
Signed-By: /usr/share/keyrings/debian-archive-keyring.gpg
```
Then update the repository

## Install GCC 15 alongside GCC 14
```
sudo apt install -t experimental libcc1-0 
sudo apt -t experimental install gcc-15 g++-15
```

Change them to default:
```
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-15 150
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-15 150
```

To change between GCC versions:
```
sudo update-alternatives --config gcc
sudo update-alternatives --config g++
```

## Install libstdc++15
Luckily libstdc++15 is automatically upgraded/installed alongside libstdc++14 while installing GCC 15. So, no need to do anything.

## Install Hypr* packages
```
wget https://github.com/imchocomint/hyprplus/blob/main/bootstrap.sh
sudo bash ./bootstrap.sh
```

## QnA
### Is it safe?
Ans: If it isn't, I wouldn't have typed this.
### Can we update to newer version?
Ans: Rerun hyprplus script again
### Why not nix (package manager)?
Ans: Can't (really) forward that to SDDM.
### Why not Guix?
Ans: This seems like a good idea. I will test it. But maybe it still requires libstdc++15 after all.
### Why not (any other distro)?
Ans: Some people have programs that works only on Debian (hell, what kind of monster would make that?) or is actively working on Debian compatability or is developing Debian, and they can't switch.

# 
So yeah. This may be the end. Thank you for reading all of this. Make sure to star this repo and share if you love it.
