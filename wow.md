# World of Warcraft in linux

This guide was tested on Ubuntu 19.10 with the following PC config
```
CPU:  Intel Core i5 2500k
GPU:  Aorus AMD RX580 5gb
Mobo: Asus P8Z68-V
RAM:  Kingston Hyper X 16gb(4x4gb) DDR3
SSD:  Adata 250gb SATA
```

## Update and upgrade
```
sudo apt update
sudo apt upgrade
```

## Install AMD open drivers
Ubuntu 19.10 comes with some of the drivers come preinstalled.
### Enable a PPA for the latest Mesa drivers.
```
sudo add-apt-repository ppa:oibaf/graphics-drivers
sudo apt update
sudo apt upgrade
```

### Install the Vulkan packages
```
sudo apt install libvulkan1 mesa-vulkan-drivers vulkan-utils
```

### Install the 32 bit drivers
```
sudo dpkg --add-architecture i386 
sudo apt install libgl1-mesa-dri:i386
sudo apt install mesa-vulkan-drivers mesa-vulkan-drivers:i386
```

## Install Lutris
Follow the Lutris [download page](https://lutris.net/downloads/) or use the instructions below.
```
sudo add-apt-repository ppa:lutris-team/lutris
sudo apt-get update
sudo apt-get install lutris
```
