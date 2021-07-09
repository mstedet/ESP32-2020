# ESP32-2020
ESP32 programerings kursus 2020


## Video list
### ESP32
* [The best input and output pins on the NodeMCU ESP32 and ESP8266](https://www.youtube.com/watch?v=c0tMGlJVmkw)
### ESP32 CAM
* [Editing Camera Web Server HTML Source Code for the ESP32-CAM](https://www.youtube.com/watch?v=bIJoVyjTf7g)
  * [Code and decode html](https://gchq.github.io/CyberChef/)
* [ESP32-CAM Take Photo and Save to MicroSD Card](https://www.youtube.com/watch?v=eot6COwCPF0)
* [Sådan opsættes og bruges ESP32 WiFi-kamera](https://www.youtube.com/watch?v=5XCb3t8J4Kg&t=293s)
* [$10 DIY Wireless IP Security Camera for 3D Printers & Home](https://www.youtube.com/watch?v=6qiH1BRwUeA)
### Home Automation
* [Home Assistant: ](https://www.home-assistant.io/)
* [Home Assistant Beginners Guide: Installation, Addons, Integrations, Scripts, Scenes, and Automations](https://www.youtube.com/watch?v=sVqyDtEjudk)  
* [Home Automation With Home Assistant and ESPHome](https://www.youtube.com/watch?v=xDbH-xPQtXU)

#### The Home Assistant Beginner’s Guide
* [Install Home Assistant](https://www.home-assistant.io/getting-started/)
* [The Home Assistant Beginner’s Guide Part 1: Setting up Hass.io](https://home-assistant-guide.com/2018/04/05/the-home-assistant-beginners-guide-part-1-setting-up-hass-io/)
* [The Home Assistant Beginner’s Guide Part 2: Web Access](https://home-assistant-guide.com/2018/05/24/the-home-assistant-beginners-guide-part-2-web-access/)
* [The Home Assistant Beginner’s Guide Part 3: Integrating Home Assistant with the Google Assistant/Google Home](https://home-assistant-guide.com/2018/05/24/the-home-assistant-beginners-guide-part-3-integrating-home-assistant-with-the-google-assistant-google-home/)

#### Home Automation With Home Assistant and ESPHome
* [Home Automation With Home Assistant and ESPHome - First Steps](https://www.youtube.com/watch?v=xDbH-xPQtXU)
  * [ESPHome](https://esphome.io/)
##### [Average Automation](https://www.youtube.com/channel/UCMR_eJdL5P6SVJ2n0kTCjlg/videos)
* [Home Assistant 101 Installing](https://www.youtube.com/watch?v=9-s8379D5vg)
* [Home assistant 102 Add-ons](https://www.youtube.com/watch?v=iNNkmFJJ6Hk)
* [Home assistant 103 ESPhome custom Relays and Temperature](https://www.youtube.com/watch?v=s3Dvl8wLPSw&list=PLyxwEDtrc_EU_AsqiN2cBUJvrhFeOGAUI&index=2)
* [Home assistant 104 ESPHome Multi sensor](https://www.youtube.com/watch?v=7RpgxiIjulw)
* DrZzs
  * [ID Card Scanner using NodeMCU, MFRC-522, esp-rfid firmware, and of course, Home Assistant](https://www.youtube.com/watch?v=ENMul9eAB00&t=2s)
  * [Get Months of Battery Life from an ESP8266!](https://www.youtube.com/watch?v=1vs86fwEdtM) 
* RC522 Arduino
  * [HausnerR / esphome-door-lock](https://github.com/HausnerR/esphome-door-lock)

  
##### IHC Controller
* [IHC Controller integration for Home Assistant](https://www.home-assistant.io/integrations/ihc/)
### YAML-filer
* [YAML | In One Video](https://www.youtube.com/watch?v=cdLNKUoMc6c&t=321s)


# Argon One M.2 - Home Assistant OS: 6.x & Supervised version
Source & Inspiration: https://community.home-assistant.io/t/raspberry-pi-4-home-assistant-os-5-5-dev-version-on-a-ssd-and-the-argon-one-m-2-case-in-progress/248025

## RPi 4b 4-8 GB Ram with M.2 SATA III boot:
* HardWare:
  * Argon One M.2 V.20
  * Raspberry Pi 4, 4-8GB Ram
  * Verbatim, 256GB Vi560 Sata III, M.2 2280 Internal SSD, Part No. 49362
  * SanDisk Ultra 16GB MicroSD-HC
  * some kind of monitor with HDMI connectors maybe a TV for installation
* SoftWare:
  * Raspberry Pi OS (32-bit), released: 2021-05-07
  * pieeprom-2021-04-29.bin
  * haos_rpi4-64-6.1 eller nyere
  * unxz
## Boot with Raspberry Pi OS (32-bit) from SD-Card:
* disconnect the built-in M.2-SATA
* boot from SD-Card 16GB with Raspberry Pi OS (32-bit), released: 2021-05-07
## Install Update:
```
sudo apt update && sudo apt full-upgrade
sudo apt-get install xz-utils
```
## Update RPi Firmware, Latest for now "pieeprom-2021-04-29.bin":
```
sudo nano /etc/default/rpi-eeprom-update

sudo rpi-eeprom-update -d -f /lib/firmware/raspberrypi/bootloader/stable/pieeprom-2021-04-29.bin
```
## Install Home Assistant OS Release 6 - (haos_rpi4):
* Connect the built-in M.2-SATA !!!
  * Home Assistant OS Release kan be found here:  
  https://github.com/home-assistant/operating-system/releases/
```
wget https://github.com/home-assistant/operating-system/releases/download/6.1/haos_rpi4-64-6.1.img.xz

unxz haos_rpi4-64-6.1.img.xz
```
## Set boot options
```
sudo raspi-config
```
* …then Boot options --> Boot Rom Version --> latest -> Ok -->
  * when the system asks to “Reset boot ROM to defaults” select No (!!!) to use the latest boot ROM.
* –> Boot Order --> USB Boot --> Ok --> Finish --> Reboot --> Shut down

## List block devices and dd - convert and copy a file:
```
lsblk
```
* i expect M.2 SATA named /dev/sda
```
sudo dd bs=4M if=haos_rpi4-64-6.1.img of=/dev/sda status=progress conv=fsync
```
## Reboot 
* If all went well it will boot Home Assistant fron SSD:
  * It will take abot 5-10 min before you can get conection to http://homeassistant.local:8123
```
reboot
```

## Argon ONE Pi 3 & 4 Cases and Fan HAT support for Home Assistant

Source & Inspiration: https://github.com/Misiu/argon40
### I2C
* [ENABLE I2C VIA HOME ASSISTANT OPERATING SYSTEM TERMINAL](https://www.home-assistant.io/common-tasks/os#enable-i2c-via-home-assistant-operating-system-terminal)
* [HassOS I2C Configurator](https://community.home-assistant.io/t/add-on-hassos-i2c-configurator/264167)