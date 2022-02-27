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

