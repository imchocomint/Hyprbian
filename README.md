# Hyprbian
The ultimate guide to install lastest Hyprland on Debian sid/trixie/experimental (since Hyprland package for Debian is super outdated)

# NOTE: Won't work on Debian 12 or lower. Untested on Ubuntu, but it should work.

## Prerequisites
- A brain to read the official documentations
- Debian 13 (trixie)/sid/experimental
- Some libraries; we'll cover them later
- Experience with make, cmake and the like
- make, cmake, rust (?)
- Patience (and maybe a good CPU)
- sway or KDE to install, as well as copy and pasting code

## Installing required libraries & dependencies (TBA)
Listed dependencies are:
- aquamarine
- hyprlang
- hyprcursor
- hyprutils
- hyprgraphics
- hyprwayland-scanner
as well as their libraries. You need a way to install them (hint: Their official GitHub repository). Or if you've been with PikaOS' repository, just install all of them.

You also need tomlplusplus and its development libraries.

For libraries, use this to install: ` sudo apt install lib<softwarename>-deb `. Replace <softwarename> with what you need.

## Install GCC 15 (not applicable to experimental)


