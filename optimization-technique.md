## Pinning Trixie (while getting package from sid)
Since some people really love Trixie (since it's currently flawless with Hyprland) but not having the choice to use dummy packages (see Installing Hyprland) and do not want to move to sid, here's a guide to pinning Trixie release:

```
sudo touch /etc/apt/preferences.d/s99sid.pref
sudo nano /etc/apt/preferences.d/s99sid.pref
```
Inside the file, paste this:
```
Package: *
Pin: release a=sid
Pin-Priority: 100

Package: *
Pin: release a=trixie
Pin-Priority: 900
```
Solution submitted by [Ddubs on JaKoolIt Discord server](https://discord.com/channels/1151869464405606400/1386170957705642126/1386562279214026803)

## Compiling hyprland-qtutils
hyprland-qtutils is a mall bunch of utility applications that hyprland might invoke like dialogs or popups.
To compile hyprland-qtutils you need some Qt dependencies: 
```
sudo apt install qt6-base-private-dev qt6-declarative-private-dev qt6-wayland-private-dev
```
Then compile like in the official guide.
