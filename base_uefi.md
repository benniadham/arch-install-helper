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

```
# arch-chroot /mnt
```
Set the timezone:
```
# ln -sf /usr/share/zoneinfo/Europe/Zurich /etc/localtime
# hwclock --systohc
```
Check the date and time:
```
# date
```

Missing packages:
git base-devel dialog wpa_supplicant linux-headers

