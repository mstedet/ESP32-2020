# Raspberry Pi OS med IOTStack 

Installer lidt programmer før installationen af Hassio
```
sudo apt install network-manager apparmor-utils
```

## 1. Clone IOTStack projected til din Raspberry
```
git clone https://github.com/SensorsIot/IOTstack.git ~/IOTStack
```
## 2. Start menu.sh
```
cd ~/IOTStack && bash ./menu.sh
```
### 1. Install Docker
reboot når du bliver spurt

### 2. Build Stack

#### 1. vælg Container
* Portainer
### 3. Install Hass.io
installer nu Homeasssistent fra IOTstack

## Start IOTstack
``` 
cd ~/IOTStack && docker-compose up -d
``` 


# VNC Connect
Download VNC® Viewer to the device you want to control from, below. Make sure you've installed VNC® Server on the computer you want to control.  

* Hent **VNC-Standalone x64** her: https://www.realvnc.com/en/connect/download/viewer/   
  * Gem filen her: ~/.local/bin/
* Hent **Real-VNC Icon** her: https://static.techspot.com/images2/downloads/topdownload/2014/06/realvnc.png  
  * Gem filen her: ~/.local/share/icons/
    * med filnavnet **real-VNC.png**
* Opret Desktop tilen **VNC-Viewer-6.20.529-Linux-x64.desktop**
  * med denne kommando 
``` 
nano ~/.local/share/applications/VNC-Viewer-6.20.529-Linux-x64.desktop
``` 
og tilføj dette indhold til desktopfilen

``` 
[Desktop Entry]
Type=Application
Name=VNC-Viewer-6.20.529-Linux-x64.desktop
Name[da_DK]=VNC-Viewer-6.20.529-Linux-x64.desktop
Comment=Flash OS images to SD cards & USB drives, safely and easily.
Icon=real-VNC.png
Exec=VNC-Viewer-6.20.529-Linux-x64
Path=
Terminal=false
StartupNotify=true
``` 
