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
* tree - directory structure
* vifm - file manager for vim
* scrot - screenshots
* shellcheck - script proofreading
* youtube-dl - video downloader
* keepass - password manager

#### AwesomeWM Autorun Script
```
chmod +x ~/.config/awesome/autorun.sh
```

#### NTP
install ntp
```
sudo systemctl enable ntpd
```

#### SSH
install openssh
```
sudo systemctl enable sshd
```

#### Wallpaper
paru pacwall

install imagemagick

#### External Disk Tools
install udisks2

paru udiskie

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

#### Sensors
install lm_sensors
```
sudo sensors-detect
```

## Laptop Specific Software
#### Battery
install acpi xf86-input-libinput

#### Brightness
install acpilight
```
vim /etc/udev/rules.d/backlight.rules
ACTION=="add", SUBSYSTEM=="backlight", KERNEL=="acpi_video0", GROUP="video", MODE="0644" 
```
