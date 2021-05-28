## Additional Software and Instructions
#
### Window Manager and Utilities
* awesome - window manager (includes panel & wallpaper)
* *awesome-freedesktop - menu for awesome
* alacritty - terminal emulator
* materia-gtk-theme - base theme
* rofi - launcher
* alsa-utils - audio utilities
* picom - compositor

### Vital Programs
* geany - text editor
* *spacefm - file manager
* firefox - web browser
* feh - image viewer
* vlc - media player
* gimp - image editor
* code - VSCode
* tree
* vifm

#### SSH
install openssh
```
sudo systemctl enable sshd
```

#### Wallpaper
* pacwall
* imagemagick

#### External Disk Tools
install udisks2 udiskie
vim /etc/udev/rules.d/99-udisks2.rules
```
ENV{ID_FS_USAGE}=="filesystem|other|crypto", ENV{UDISKS_FILESYSTEM_SHARED}="1"
```

#### Numlock Set at Login
install numlockx
vim /etc/lightdm/lightdm.conf
under [Seat:*]
```
greeter-setup-script=/usr/bin/numlockx on
```
