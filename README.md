# Arch-Install
## Installation Instructions - Arch EFI
#
#### Set Key Mode
```
loadkeys us
```
#### Verify Boot Mode
```
ls /sys/firmware/efi/efivars
```
###### If no errors -> running in EFI mode
#
#### Enter Wifi Setup
```
iwctl
```
#### List Devices
```
device list
```
#### Scan for Networks
```
station <device> scan
```
#### List Networks
```
station <device> get-networks
```
#### Connect to Network
```
station <device> connect <SSID>
```
#### Exit Wifi Setup
```
exit
```
#### Test Connection
```
ping google.com
```

#

#### Update System Clock
```
timedatectl set-ntp true
```
#### Verify
```
timedatectl status
```
#
#### List Disks
```
fdisk -l
```
#### Enter Disk Setup
```
fdisk /dev/sdX
```
#### Create New Partition Table (EFI = GPT)
```
g
```
#### Create Boot Partition
###### commas = series of prompt responses
```
n, 1, <default>, +550M
```
#### Create Swap Partition
```
n, 2, <default>, +2G
```
#### Create Root Partition
```
n, 3, <default>, <default>
```
#### Change Boot Partition Type
```
t, 1, L, (EFI System)
```
#### Change Swap Partition Type
```
t, 2, L, (Linux Swap)
```
#### Change Root Partition Type
```
t, 3, L, (Linux Filesystem)
```
#### Write Partition Table
```
w
```
#
#### Make Boot Filesystem
```
mkfs.fat -F32 /dev/sdX1
```
#### Make Swap Filesystem
```
mkswap /dev/sdX2
```
#### Activate Swap
```
swapon /dev/sdX2
```
#### Make Root Filesystem
```
mkfs.ext4 /dev/sdX3
```
#

#### Mount Root Filesystem
```
mount /dev/sdX3 /mnt
```
#### Install Base System
```
pacstrap /mnt base linux linux-firmware
```
#### Generate Fstab
```
genfstab -U /mnt >> /mnt/etc/fstab
```
#
#### Enter New Root Filesystem
```
arch-chroot /mnt
```
#### Install Vim and Sudo
```
pacman -S vim sudo
```
#### Set Timezone
```
ln -sf /usr/share/zoneinfo/America/New_York /etc/localtime
```
#### Set System Clock
```
hwclock --systohc
```
#### Set Locale
```
vim /etc/locale.gen
```
###### uncomment 'en_US.UTF-8'
```
locale-gen
```
#### Set Hostname
vim /etc/hostname
```
<hostname>
```
vim /etc/hosts
```
127.0.0.1    localhost
::1          localhost
127.0.1.1    <hostname>.localdomain    <hostname>
```
#

#### Setup Root User
```
passwd
```
###### enter root password
#### Setup User
```
useradd -m <user>
passwd <user>
```
###### enter user password
#### Add User to Sudoers
```
usermod -aG wheel,audio,video,storage <user>
visudo
```
###### uncomment line '%wheel ALL=(ALL) ALL'
#
#### Mount Boot Partition
```
mkdir /boot/EFI
mount /dev/sdX1 /boot/EFI
```
#
#### Install Grub and EFI tools
```
pacman -S grub efibootmgr dosfstools os-prober mtools base-devel nfts-3g
```
#### Add Grub
```
grub-install --target=x86_64-efi --bootloader-id=grub_uefi --recheck
```
#### Configure Grub
```
grub-mkconfig -o /boot/grub/grub.cfg
```
#### Remove Grub Countdown
```
vim /etc/default/grub
```
###### change countdown from 5 to 0
#### Save Configuration
```
grub-mkconfig -o /boot/grub/grub.cfg
```
#
#### Add Additional Packages
```
pacman -S networkmanager git wget bash unzip unrar rsync samba cronie python-pip exfat-utils
```
#### Enable Network Manger
```
systemctl enable NetworkManager
```
#
#### Exit Installer
```
exit
umount -l /mnt
```
#
### Shutdown and Remove Installation Media
### Base Install Complete
##

# Install GUI

#### Configure Network Manager for Wifi
```
nmcli device wifi connect <SSID> password <password>
```
#### Install Video Driver
###### consult the wiki -_-
#### Install Xorg
```
sudo pacman -S xorg
```
#### Install Login Manager
```
sudo pacman -S lightdm lightdm-gtk-greeter
sudo systemctl enable lightdm
```
#### Install Paru for AUR Installation
```
git clone https://aur.archlinux.org/paru.git
cd paru
makepkg -sri
```

[Add additional software as needed](../Additional-Software.md)
