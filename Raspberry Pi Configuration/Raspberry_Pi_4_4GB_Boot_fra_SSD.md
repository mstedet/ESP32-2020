# Raspberry Pi 4, Homeassistant installeret via docker
## Kilder:  
* [#352 Raspberry Pi4 Home Automation Server (incl. Docker, OpenHAB, HASSIO, NextCloud)](https://www.youtube.com/watch?v=KJRMjUzlHI8)
* [#341 Quickie: Raspberry Pi official USB Boot now much simpler. How fast is a cheap SSD?](https://www.youtube.com/watch?v=8vC3D19e_Ac)
* [#295 Raspberry Pi Server based on Docker, with VPN, Dropbox backup, Influx, Grafana, etc: IOTstack](https://www.youtube.com/watch?v=a6mjt8tWUws&feature=youtu.be)

## Installer Raspberry Pi Imager
Brug Raspberry Pi Imager til en nem måde at installere Raspberry Pi OS og andre operativsystemer på et SD-kort klar til brug sammen med din Raspberry Pi:

* [Raspberry Pi Imager til Windows](https://downloads.raspberrypi.org/imager/imager_1.4.exe)  
* [Raspberry Pi Imager til macOS](https://downloads.raspberrypi.org/imager/imager_1.4.dmg)
* [Raspberry Pi Imager til Ubuntu](https://downloads.raspberrypi.org/imager/imager_1.4_amd64.deb)  
Installer Raspberry Pi Imager til Raspberry Pi OS ved at køre 
``` sudo apt install rpi-imager ```
i et terminalvindue

## Flash SD kort
* Operating System vælges "Raspberry Pi OS (32-bit)" (Recommended)  
![Raspberry Pi Imager_OS](./Images/Raspberry_PI_Imager_OS.png)
* SD Card vælges det du ønsker at boote fra  
![Raspberry_Pi_Imager_CD_Card.png](./Images/Raspberry_Pi_Imager_CD_Card.png)
* Vælg Write for at overfører Raspberry Pi OS til SD-Kortet  
![Raspberry Pi Imager](./Images/Raspberry_Pi_Imager.png)
* Skrivebprsessen er nu færdig tryk [CONTINUE]  
![Raspberry_Pi_Imager_Done.png](./Images/Raspberry_Pi_Imager_Done.png)
* SD-Kortet kan indsættes i din Raspberry Pi 4  

## Boot Raspberry fra SD-Kort
* Indsætte SD-kortet i din Raspberry PI 
* Forbind nu micro HDMI stikket til en skærm eller TV's HDMI med  [Micro HDMI til HDMI Adapter](https://raspberrypi.dk/produkt/micro-hdmi-til-hdmi-adapter-235mm-hvid/)
* Forbind strømforsyningen og du kan tænde

## Config Raspberry Pi OS til boot fra USB-Disk i stedet for SD-Kort
### 1. Opdater Raspberry Pi OS til nyeste filer & Opdater Raspberry Pi EEProm
* Åben et terminal vindue og opdater Raspberry PI OS til nyeste version med disse kommandoer:
```
sudo apt update && sudo apt full-upgrade
```
* Check om **stable release** er valgt, åben filen **/etc/default/rpi-eeprom-update** og ret indhold til **FIRMWARE_RELEASE_STATUS="stable"**, brug nano editoren til dette:
```
sudo nano /etc/default/rpi-eeprom-update
```
* Check for release version med denne kommando:
```
sudo rpi-eeprom-update -d -a
```
* List nu alle dine eeprom versioner, brug den nyeste
```
ls /lib/firmware/raspberrypi/bootloader/stable/
``` 
* Opdater nu eeprommen med denne kommando:
```
sudo rpi-eeprom-update -d -f /lib/firmware/raspberrypi/bootloader/stable/pieeprom-2020-09-03.bin
```
* Reboot nu 
### 2. Start Raspberry Pi OS config program
* Start Raspberry config med denne kommando:
```
sudo raspi-config
```
#### 1. Set Boot Option  
* Vælg Boot Option  
![RasPi_3_Boot_Option.png](./Images/RasPi_3_Boot_Option.png)  
* Vælg Boot ROM version  
![RasPi_B5_Boot_Rom_Version.png](./Images/RasPi_B5_Boot_Rom_Version.png)
* vælg Latest  
![RasPi_E1_Latest.png](./Images/RasPi_E1_Latest.png)
* Vælg Nej  
![RasPi_Latest_Nej.png](./Images/RasPi_Latest_Nej.png)
#### 2. Set Boot Order
* Vælg Boot Order  
![RasPi_3_Boot_Option.png](./Images/RasPi_3_Boot_Option.png) 
* Vælg USB Boot  
* ![RasPi_B1_USB_Boot.png](./Images/RasPi_B1_USB_Boot.png) 
* Vælg OK  
* ![RasPi_USB_Device_is_default.png](./Images/RasPi_USB_Device_is_default.png) 
* Vælg Finish   
![RasPi_Select_Finish.png](./Images/RasPi_Select_Finish.png)  
* vælg Ja for Reboot af Raspbery Pi
* ![Raspi_Reboot_Now.png](./Images/Raspi_Reboot_Now.png) 
### 3.
* Indsæt USB Disk og behold SD-kort jeg bruger denne adapter til SSD-Disk [USB 3.0 til SATA 6Gb/s adapter - 2,5"/3,5"](https://www.av-cables.dk/usb-3-0-til-sata-adapter/usb-3-0-til-sata-6gb-s-adapter-2-5-3-5.html), da Raspberry Pi ikke kan levere strøm nok til disken, min SSD-Disk er [Kingston A400 240GB SSD SATA](https://www.proconsult.dk/product/hd-sa400s37-240g/kingston-a400-240gb-ssd-sata)
* For a kopier SD-Kort til SSD-Disk
  1. Åben Paspberry Pi OS menu Tilbehør -> SD Card Copier
  2.  Sluk din Raspberry Pi når kopieringen er slut
  3.  Fjern SD-Kort
* Boot nu fra SSD-Disk,  
og alt bør starte som var det et SD-Kort
