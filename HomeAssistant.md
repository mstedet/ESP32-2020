# Vejledninger til HomeAssistant 2021

## Home Assistant Raspberry Pi 4 SSD Installation and Migration
* [Everything Smart Home](https://www.youtube.com/watch?v=QxtDyMbDOh4)
### Software til brug for installationen
* Raspberry Pi Imager
afinstaller gammel version med komandoen:
```
sudo apt remove rpi-imager
```
og installer nyeste version med kommandoen
```
sudo snap install rpi-imager
```
### Klargør din SSD disk for Home Assistant, jeg bruger en JMicron Tech UB til ATA adapter og tilslutter min SSD via USB3 på min PC.
* CHOOSE OS: --> Other specific purpose OS -->
  * Select: Home Assistant --> Home Assistant OS 5.13 (RPI4/400)
* CHOOSE STORAGE: -->> JMicron Tech 
* WRITE: --> YES

### Klargør SD-Kort til at sætte Rasperry PI til Boote fra USD-Drev, jeg bruger et 8.0GB SD-Kort
* CHOOSE OS: --> Misc utility Images --> 
  * Select: Bootloader --> USB Boot
* CHOOSE STORAGE: -->> Generic STORAGE_DEVICE - 8.0GB
* WRITE: --> YES

## Add-on Store
* File editor
```
dirsfirst: false
enforce_basepath: true
git: true
ignore_pattern:
  - __pycache__
  - .cloud
  - .storage
  - deps
ssh_keys: []
``` 
* ESPHome
* Samba share
  * Configuration Options
```
workgroup: WORKGROUP
username: sekt1953
password: XQMyQ#2A.52Y
interface: ''
allow_hosts:
  - 10.0.0.0/8
  - 172.16.0.0/12
  - 192.168.0.0/16
  - fe80::/10
veto_files:
  - ._*
  - .DS_Store
  - Thumbs.db
  - icon?
  - .Trashes
compatibility_mode: false

```
* MariaDB 
  * Home Assistant MariaDB Install and System Monitoring
    * [Home Assistant MariaDB Install and System Monitoring](https://www.youtube.com/watch?v=FbFyqQ3He7M) af Everything Smart Home
```
databases:
  - homeassistant
logins:
  - username: homeassistant
    password: z8wvgwg3thwhqnfc
rights:
  - username: homeassistant
    database: homeassistant
```

* SSH
  * [Enable SSH In Home Assistant - TUTORIAL 2021](https://www.youtube.com/watch?v=_ANmn9QSLtA) af Smart Home Junkie

* HACS
  * [How to install HACS in 2021 in Home Assistant - NEW UPDATED VERSION!](https://www.youtube.com/watch?v=D6ZlhE-Iv9E)

```
/config/custom_components
```





















# Video og vejledninger om HomeAssistant 
## Se videoerne læs teksterne før du går igang med installation 
jeg har valg disse videoer og vejledninger fordi de viseer os en måde at bruge vores ESP32 i hvores hjem. 
* [By Juan](https://www.juanmtech.com/)
  * [Beginner’s Guide to Home Assistant](https://www.juanmtech.com/guide-to-home-assistant/)
  * [Home Assistant – Beginner’s guide Based on HassOS](https://www.juanmtech.com/home-assistant-hassos-beginners-guide/)
  * [How to set up themes in Home Assistant](https://www.juanmtech.com/themes-in-home-assistant/)
  * [How to set up Lovelace on Home Assistant](https://www.juanmtech.com/how-to-set-up-lovelace-on-home-assistant/)
  * [How to set up the Picture Elements card in Home Assistant – Lovelace](https://www.juanmtech.com/set-up-the-picture-elements-card-in-home-assistant/)
  * [Home Assistant new user interface and UI editor](https://www.juanmtech.com/home-assistant-new-user-interface-and-ui-editor/)
  * [How to get started with ESPHome and Sonoff](https://www.juanmtech.com/how-to-get-started-with-esphome-and-sonoff/)
* [by misperry](https://www.youtube.com/channel/UCWL128ZuBbV8ruKrc0lk7Iw)
  * [Setting up Home Assistant Lovelace UI](https://www.youtube.com/watch?v=QEtX0uboxQA)
* [Vaclav Chaloupka](https://www.youtube.com/channel/UCA5DCnztFFHgdEettFHZ2Kw)
  * [Living with Home Assistant](https://www.youtube.com/watch?v=eaPAhYscCZw)
  * [Home Assistant](https://www.youtube.com/watch?v=eaPAhYscCZw&list=PLhvGKnQhU0T0_bioWuwImEsZuLScNKd-i)
## Dokumentation

![HA-logo](/Images/HA-Logo.png) 
* [Home Assistant Documentation](https://www.home-assistant.io/docs/)  
* [Lovelace UI](https://www.home-assistant.io/lovelace/)
  * [Customizing entities](https://www.home-assistant.io/docs/configuration/customizing-devices/)
  * [Material Design Icons](https://cdn.materialdesignicons.com/4.5.95/)  
* [Automating Home Assistant](https://www.home-assistant.io/docs/automation/)

![EspHome-logo](/Images/ESPHome-logo.png)
* [ESPHome](https://esphome.io/)  

# Min Test installation på en Raspberry Pi 4 
## Installations filer hentes her
* [Installing Home Assistant](https://www.home-assistant.io/hassio/installation/)
  * Raspberry Pi 3
    * [Raspberry Pi 3 Model B and B+ 32bit (recommended)](https://github.com/home-assistant/operating-system/releases/download/3.13/hassos_rpi3-3.13.img.gz)
    * Raspberry Pi 3 Model B and B+ 64bit](https://github.com/home-assistant/operating-system/releases/download/3.13/hassos_rpi3-64-3.13.img.gz)    
  * Raspberry Pi 4
    * [Raspberry Pi 4 Model B 32bit (recommended)](https://github.com/home-assistant/operating-system/releases/download/3.13/hassos_rpi4-3.13.img.gz)
    * [Raspberry Pi 4 Model B 64bit](https://github.com/home-assistant/operating-system/releases/download/3.13/hassos_rpi4-64-3.13.img.gz)
  * VirtualBox PC/Mac
    * [VDI for Virtualbox installation](https://github.com/home-assistant/operating-system/releases/download/3.13/hassos_ova-3.13.vdi.gz)
* balenaEtcher et flash program 
  * [balenaEtcher vælg system](https://www.balena.io/etcher/)
  
## Supervisor Add-on store
### Terminal $ SSH
Configuration:
```
authorized_keys:
  - >-
    ssh-rsa
    AAAAB3NzaC1yc2EAAAADAQABAAABAQCxuzaCFj1J7Jf7r9NqPGtmHoSF....
password: ''
```
Network
```
22
```
Access fra linux terminal:
```
ssh root@homeassistant.local
```
### Samba
Configuration:
```
workgroup: WORKGROUP
username: admin
password: password
interface: ''
allow_hosts:
  - 10.0.0.0/8
  - 172.16.0.0/12
  - 192.168.0.0/16
  - 'fe80::/10'
veto_files:
  - ._*
  - .DS_Store
  - Thumbs.db
  - icon?
  - .Trashes
compatibility_mode: false
```
Mount SMB fra Linux
```
smb://admin@homeassistant.local/config
```
### File editor
Configuration:
```
dirsfirst: false
enforce_basepath: true
ignore_pattern:
  - __pycache__
  - .cloud
  - .storage
  - deps
ssh_keys: []
```
### ESPHome
Manage add-on repositories
```
https://github.com/esphome/hassio
```
Configuration:
```
```
### Visual Studio Code kun på 64bit version
Configuration:
```
```

```
```
