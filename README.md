# So you decided to screw up big time

### Bare Necessities

1. `archfi` 
2. `gnome`
3. `neofetch`
4. `b43-fwcutter b43-firmware`
5. `base-devel`
6. `yay`
7. `fish`
8. `cutefish-icons cutefish-wallpapers`
9. `flatpak`
10. Orchis Theme & Volantes Cursors
11. `vlc`
12. `lightdm-webkit2-greeter`
13. `gnome-tweaks`

    

### Development

1. `nodejs npm`
2. `go`
3. `visual-studio-code-bin`
4. `jdk-openjdk`
5. Android Studio
6. JetBrains Mono
7. `kite`
8. `inkscape gimp`

       



### Luxuries

1. `brave-bin`
2. `freedownloadmanager`
3. `cava`
4. `typora`
5. `insomnia`
6. `balena-etcher`
7. `telegram-desktop`




## Minor Configs

### LightDM

[Arch Wiki reference](https://wiki.archlinux.org/title/LightDM)

```sh
# edit /etc/lightdm/lightdm.conf
[Seat:*]
...
greeter-session=lightdm-webkit2-greeter
...
```

## Resources
[cutefish-wallpapers](https://github.com/cutefishos/wallpapers)



```sh
# add folders that contain configs for future builds of each DE/WM and folders for wallpapers
# create a back-up for my music on google drive
```

## Install arch linux
Using fdisk:
```sh
fdisk -l   (lists out the partitions)
fdisk /dev/sda  
In fdisk, "m" for help
In fdisk, "o" for DOS partition or "g" for GPT
In fdisk, "n" for add new partition
In fdisk, "p" for primary partition (if using MBR instead of GPT)
In fdisk, "t" to change partition type
In fdisk, "w" (write table to disk)
```

Make filesystem:
```sh
mkfs.fat -F32 /dev/sda1
mkswap /dev/sda2
swapon /dev/sda2
mkfs.ext4 /dev/sda3
```

Base Install:
```sh
mount /dev/sda3 /mnt (mounts it to mnt on live image)
pacstrap /mnt base linux linux-firmware
genfstab -U /mnt >> /mnt/etc/fstab (YouTube doesn't allow angle brackets)
```
Chroot:
```sh
arch-chroot /mnt (change into root directory of our new installation)
ln -sf /usr/share/zoneinfo/Africa/Nairobi /etc/localtime
hwclock --systohc (sets the hardware clock)
pacman -S nano
nano /etc/locale.gen
locale-gen
nano /etc/hostname
nano /etc/hosts
```

Users and passwords:
```sh
passwd (set root pass)
useradd -m username (make another user)
passwd username (set that user's password)
usermod -aG wheel,audio,video,optical,storage username
```
Sudo:
```sh
pacman -S sudo
EDITOR=nano visudo
```
GRUB:
```sh
pacman -S grub
pacman -S  efibootmgr dosfstools os-prober mtools (if doing UEFI)
mkdir /boot/EFI (if doing UEFI)
mount /dev/sda1 /boot/EFI  #Mount FAT32 EFI partition (if doing UEFI)
grub-install --target=x86_64-efi  --bootloader-id=grub_uefi --recheck (if doing UEFI)
grub-mkconfig -o /boot/grub/grub.cfg
```

Networking:
```sh
pacman -S networkmanager
systemctl enable NetworkManager
```
Reboot:
exit the chroot by typing "exit"
```sh
umount /mnt (unmounts /mnt)
```
reboot (or shutdown now if doing this in VirtualbBox)
Remember to detach the ISO in VirtualBox before reboot.

