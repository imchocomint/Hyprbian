We're archiving this repo. Everything will be/have already been moved to https://github.com/imchocomint/hyprplus. Thank you.

# Painless Hyprbian
The ultimate guide to install lastest Hyprland on Debian sid/experimental (since Hyprland package for Debian is super outdated), using relatively dark magic.

# NOTE: Won't work on Debian 12 or lower. Will works on Debian 13 using custom/backported packages, but we don't support that.

# NOTE 2: If you're using Debian trixie, please consider carefully before following this guide. You're going to make your system a [FrankenDebian](https://wiki.debian.org/SourcesList#Precautions).


## Prerequisites
- A brain to read the official documentations
- Debian sid/experimental, Ubuntu 25.10 and everything based on that
- sway or KDE to install, as well as copy and pasting code

## Adding unstable (sid) repo (for trixie users)
Update: We stopped supporting Debian trixie so you will be on your own on this.

## Install GCC 15
### For Debian trixie
Install packages gcc-15 and g++-15

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

### For Debian sid/experimental
`sudo apt full-upgrade`

The August 11 package updates added GCC 15 and G++ 15 to sid repo.

## Install libstdc++15
Luckily libstdc++15 is automatically upgraded/installed alongside libstdc++14 while installing GCC 15. So, no need to do anything.

## Install Hypr* packages
Refer to https://github.com/imchocomint/hyprplus

## QnA
### Can we update to newer version?
Ans: Rerun hyprplus script again

# 
So yeah. This may be the end. Thank you for reading all of this. Make sure to star this repo and share if you love it.
