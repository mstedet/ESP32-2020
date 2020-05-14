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
smb://admin@homeassistant/config
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
