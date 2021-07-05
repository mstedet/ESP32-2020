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


# Argon One M.2 - Home Assistant version: 6.x - Supervised version
Guide Here : https://community.home-assistant.io/t/raspberry-pi-4-home-assistant-os-5-5-dev-version-on-a-ssd-and-the-argon-one-m-2-case-in-progress/248025

## RPi 4b with M.2 SATA III boot
* HardWare:
  * Argon One M.2 V.20
  * Verbatim, 256GB Vi560 Sata III, M.2 2280 Internal SSD, Part No. 49362
  * SanDisk Ultra 16GB MicroSD-HC
* SoftWare:
  * Raspberry Pi OS (32-bit), released: 2021-05-07
  * hassos_rpi4-64-5.5.img.gz
```
sudo apt update && sudo apt full-upgrade

sudo nano /etc/default/rpi-eeprom-update

sudo rpi-eeprom-update -d -f /lib/firmware/raspberrypi/bootloader/stable/pieeprom-yyyy-mm-dd.bin

sudo rpi-eeprom-update -d -a

sudo raspi-config
```

…then Boot options --> Boot Rom Version --> latest -> Ok -->
when the system asks to “Reset boot ROM to defaults” select No (!!!) to use the latest boot ROM.
–> Boot Order --> USB Boot --> Ok --> Finish --> Reboot --> Shut down
```
wget https://github.com/home-assistant/operating-system/releases/download/5.5/hassos_rpi4-64-5.5.img.gz

gzip -d hassos_rpi4-64-5.5.img.gz


lsblk

sudo dd bs=4M if=hassos_rpi4-64-5.5.img of=/dev/sda status=progress conv=fsync

```

## [Argon ONE Pi 3 & 4 Cases and Fan HAT support for Home Assistant](https://github.com/Misiu/argon40)

