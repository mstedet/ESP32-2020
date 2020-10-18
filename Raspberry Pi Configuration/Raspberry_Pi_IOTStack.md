# Raspberry Pi OS med IOTStack 

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
Installer lidt programmer før installationen af Hassio
```
sudo apt install network-manager apparmor-utils
```


## Start IOTstack
``` 
cd ~/IOTStack && docker-compose up -d
``` 


# VNC Connect
Download VNC® Viewer to the device you want to control from, below. Make sure you've installed VNC® Server on the computer you want to control.  
https://www.realvnc.com/en/connect/download/viewer/


~/.local/share/applications/VNC-Viewer-6.20.529-Linux-x64.desktop
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
