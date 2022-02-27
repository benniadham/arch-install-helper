## A. Preparation
### 1. Setup Wireless Network
Run:
```
# iwctl
```
* Type `device list` and press enter to get the list of available devices
* Type `station [device name] scan` and press enter to scan the network.
* Type `station [device name] get-neworks` and press enter to get the list or available networks.
* Type `station [device name] connect [network name]` and press enter to try and join the network. Enter password if asked.

### 2. Resize Terminal Font
Update pacman databases and install the font:
```
# pacman -Sy
# pacman -S terminus-font
```
If needed, get the font config package:
```
# pacman -S fontconfig
```
Update font cache and then set for to a larger size:
```
# fc-cache -fv
# setfont ter-v32b
```
### 3. Synchronize Time 
```
# timedatectl set-ntp true
```
## Set Partition
Delete:
```
fdisk /dev/nvme0n1
```
Create:
```
fdisk /dev/nvme0n1
```
Make file system for `/`:
```
# mkfs.ext4 /dev/nvme0n1p3
```
Make swap parition:
```
# mkswap /dev/nvme0n1p2
# swapon /dev/nvme0n1p2
```

Mount the partition for installation:
```
# mount /dev/nvme0n1p3 /mnt
```

Install base packages:
```
# pacstrap /mnt base linux linux-firmware inter-ucode
```

Generate `fstab` file:
```
# genfstab -U /mnt >> /mnt/etc/fstab
```

Check the fstab:
```
# cat /mnt/etc/fstab
```

## C. Installation
### 1. Setup
```
# arch-chroot /mnt
```

### 2 Set the timezone
Select timezone
```
# tzselect
```
Set your timezone:
```
# ln -sf /usr/share/zoneinfo/Europe/Zurich /etc/localtime
```
Synch time:
```
# hwclock --systohc --utc
```
Check the date and time:
```
# date
```

Install an editor:
```
pacman -S nano
```

Edit /etc/locale.gen: uncomment en_US.UTF-8 (Or locale of you choice)
```
# nano /etc/locale.gen
```
Generate locale:
```
# locale-gen
```
Edit locale.conf:
```
# echo LANG=en_US.UTF-8 > /etc/locale.conf
```
Set hostname:
```
# echo my_hostname > /etc/hostname
```
Edit hosts:
```
# nano /etc/hosts
```
Enter the following:
```
127.0.0.1       localhost
::1             localhost
127.0.1.1       myhost.localdomain    myhost
```



Missing packages:
git base-devel dialog wpa_supplicant linux-headers

