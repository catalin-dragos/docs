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

## Install the game
* create a lutris account so you can sync your games.  
* search for World of Warcraft and add it to your library.  
* sign in to lutris on your destop and sync your library.  
* during the installation process you will be asked to install different dependencies. 
* press OK/Proceed for all of them.  
* it will ask for the battle.net dependecy.  
* during that, it will ask for login details.  
* **DO NOT ENTER THEM** and close the login dialog.  
* let the installation finish.
* change the wine runner to the latest version
* change the game runner to one you just installed
* make sure it usus DXVK and make sure it uses the latest version available from the dropdown list
* enable VKD3D and Esync
* in system options `Disable desktop effects`
* add `DXVK_FAKE_DX10_SUPPORT` with a value of `1`
* add `mesa_glthread` with a value of `true`
* go the the `Wine configuration` and make sure compatibility is set to Windows 10

## Game issues
### Input is broken
Mouse input may interfere with the keyboard input so make sure to run this command in the actual game chat:  
```
/console rawMouseEnable 1
```

### Low fps
Make sure WoW is running in DX11 mode and **not** DX12. This can be found in the advanced settings tab in game.  
Also running this command in game might also help:  
```
/console worldPreloadNonCritical 0 
```
### Screen Tearing
You'll need to enable AMD TearFree.  
Check that you are using the `amdgpu` driver using this command and checking which driver is in use.
```
lspci -nnk | grep -i -EA3 "3d|display|vga"
```
Then create this file in which you'll add the config
```
/etc/X11/xorg.conf.d/20-amdgpu.conf
```
This is the config you need
```
Section "Device"
        Identifier "AMD"
        Driver  "amdgpu"
        Option "TearFree" "true"
EndSection
```

## Helpful links
1. [Screen Tearing Fix Video](https://www.youtube.com/watch?v=WWg8q_f7nI4)
2. [Lutris WoW GitHub page](https://github.com/lutris/lutris/wiki/Game:-World-of-Warcraft)
3. [Vulkan drivers on linux](https://linuxconfig.org/install-and-test-vulkan-on-linux)
4. [Lutris GitHub wiki drivers page](https://github.com/lutris/lutris/wiki/Installing-drivers)
