# ![realvnc64.png](./Images/realvnc64.png) VNC Connect
Download VNC® Viewer to the device you want to control from, below. Make sure you've installed VNC® Server on the computer you want to control.  

* Hent **VNC - Standalone x64** her: https://www.realvnc.com/en/connect/download/viewer/   
  * Gem filen her: ~/.local/bin/
* Hent **Real-VNC Icon** ![realvnc32.png](./Images/realvnc32.png) med denne kommando:
``` 
wget https://static.techspot.com/images2/downloads/topdownload/2014/06/realvnc.png -O ~/.local/share/icons/real-VNC.png
``` 
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
