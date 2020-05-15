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
# EspHome

## Edit /confoig/esphome/secrets.yaml
```
my_ssid_id: "Dit Netværks SSID"
my_ssid_pass: "Dit Netværks password"
```
## Create a configuration file
* Introduction And Name
  * Device Name: esp32_sonoff
* Device Type
  * Device Type: Espressif ESP32 Dev Module
* WiFi And Over-The_Air Updates
  * WiFi SSID: !secret my_ssid_id
  * WiFi Password: !secret my_ssid_pass
  * Access Password:
* Done

Nu er der brug for at rette lidt i filen
```
wifi:
  ssid: "!secret my_ssid_id"
  password: "!secret my_ssid_pass"
```
Rettes til 
```
wifi:
  ssid: !secret my_ssid_id
  password: !secret my_ssid_pass
```
vælg Save Close
## Compile and Upload esp32_sonoff.yaml to /dev/ttyUSB0 (CP2102 USB to UART Bridge Controller):
resultatet skulle line dette:
```
INFO Reading configuration /config/esphome/esp32_sonoff.yaml...
INFO Generating C++ source...
INFO Compiling app...
INFO Running:  platformio run -d /config/esphome/esp32_sonoff
Processing esp32_sonoff (board: esp32dev; framework: arduino; platform: espressif32@1.11.0)
--------------------------------------------------------------------------------
HARDWARE: ESP32 240MHz, 320KB RAM, 4MB Flash
Dependency Graph
|-- <AsyncTCP-esphome> 1.1.1
|-- <ESPmDNS> 1.0
|   |-- <WiFi> 1.0
|-- <FS> 1.0
|-- <ESPAsyncWebServer-esphome> 1.2.6
|   |-- <AsyncTCP-esphome> 1.1.1
|   |-- <FS> 1.0
|   |-- <WiFi> 1.0
|-- <DNSServer> 1.1.0
|   |-- <WiFi> 1.0
|-- <Update> 1.0
|-- <WiFi> 1.0
Compiling /data/esp32_sonoff/.pioenvs/esp32_sonoff/src/main.cpp.o
Linking /data/esp32_sonoff/.pioenvs/esp32_sonoff/firmware.elf
Retrieving maximum program size /data/esp32_sonoff/.pioenvs/esp32_sonoff/firmware.elf
Checking size /data/esp32_sonoff/.pioenvs/esp32_sonoff/firmware.elf
Building /data/esp32_sonoff/.pioenvs/esp32_sonoff/firmware.bin
DATA:    [=         ]  12.9% (used 42320 bytes from 327680 bytes)
PROGRAM: [=====     ]  53.1% (used 870286 bytes from 1638400 bytes)
========================= [SUCCESS] Took 22.70 seconds =========================
INFO Successfully compiled program.
INFO Running:  platformio run -d /config/esphome/esp32_sonoff -t upload --upload-port /dev/ttyUSB0
Processing esp32_sonoff (board: esp32dev; framework: arduino; platform: espressif32@1.11.0)
--------------------------------------------------------------------------------
HARDWARE: ESP32 240MHz, 320KB RAM, 4MB Flash
Dependency Graph
|-- <AsyncTCP-esphome> 1.1.1
|-- <ESPmDNS> 1.0
|   |-- <WiFi> 1.0
|-- <FS> 1.0
|-- <ESPAsyncWebServer-esphome> 1.2.6
|   |-- <AsyncTCP-esphome> 1.1.1
|   |-- <FS> 1.0
|   |-- <WiFi> 1.0
|-- <DNSServer> 1.1.0
|   |-- <WiFi> 1.0
|-- <Update> 1.0
|-- <WiFi> 1.0
Retrieving maximum program size /data/esp32_sonoff/.pioenvs/esp32_sonoff/firmware.elf
Checking size /data/esp32_sonoff/.pioenvs/esp32_sonoff/firmware.elf
DATA:    [=         ]  12.9% (used 42320 bytes from 327680 bytes)
PROGRAM: [=====     ]  53.1% (used 870286 bytes from 1638400 bytes)
Configuring upload protocol...
AVAILABLE: esp-prog, espota, esptool, iot-bus-jtag, jlink, minimodule, olimex-arm-usb-ocd, olimex-arm-usb-ocd-h, olimex-arm-usb-tiny-h, olimex-jtag-tiny, tumpa
CURRENT: upload_protocol = esptool
Looking for upload port...
Use manually specified: /dev/ttyUSB0
Uploading /data/esp32_sonoff/.pioenvs/esp32_sonoff/firmware.bin
Serial port /dev/ttyUSB0
Connecting.....
Chip is ESP32D0WDQ6 (revision 1)
Features: WiFi, BT, Dual Core, Coding Scheme None
MAC: 30:ae:a4:37:42:28
Uploading stub...
Running stub...
Stub running...
Changing baud rate to 460800
Changed.
Configuring flash size...
Auto-detected Flash size: 4MB
Compressed 15872 bytes to 10319...

Writing at 0x00001000... (100 %)
Wrote 15872 bytes (10319 compressed) at 0x00001000 in 0.2 seconds (effective 528.5 kbit/s)...
Hash of data verified.
Compressed 3072 bytes to 143...

Writing at 0x00008000... (100 %)
Wrote 3072 bytes (143 compressed) at 0x00008000 in 0.0 seconds (effective 2716.1 kbit/s)...
Hash of data verified.
Compressed 8192 bytes to 47...

Writing at 0x0000e000... (100 %)
Wrote 8192 bytes (47 compressed) at 0x0000e000 in 0.0 seconds (effective 9194.8 kbit/s)...
Hash of data verified.
Compressed 870400 bytes to 485930...

Writing at 0x00010000... (3 %)
Writing at 0x00014000... (6 %)
Writing at 0x00018000... (10 %)
Writing at 0x0001c000... (13 %)
Writing at 0x00020000... (16 %)
Writing at 0x00024000... (20 %)
Writing at 0x00028000... (23 %)
Writing at 0x0002c000... (26 %)
Writing at 0x00030000... (30 %)
Writing at 0x00034000... (33 %)
Writing at 0x00038000... (36 %)
Writing at 0x0003c000... (40 %)
Writing at 0x00040000... (43 %)
Writing at 0x00044000... (46 %)
Writing at 0x00048000... (50 %)
Writing at 0x0004c000... (53 %)
Writing at 0x00050000... (56 %)
Writing at 0x00054000... (60 %)
Writing at 0x00058000... (63 %)
Writing at 0x0005c000... (66 %)
Writing at 0x00060000... (70 %)
Writing at 0x00064000... (73 %)
Writing at 0x00068000... (76 %)
Writing at 0x0006c000... (80 %)
Writing at 0x00070000... (83 %)
Writing at 0x00074000... (86 %)
Writing at 0x00078000... (90 %)
Writing at 0x0007c000... (93 %)
Writing at 0x00080000... (96 %)
Writing at 0x00084000... (100 %)
Wrote 870400 bytes (485930 compressed) at 0x00010000 in 12.3 seconds (effective 566.8 kbit/s)...
Hash of data verified.

Leaving...
Hard resetting via RTS pin...
========================= [SUCCESS] Took 25.39 seconds =========================
INFO Successfully uploaded program.
INFO Starting log output from /dev/ttyUSB0 with baud rate 115200
[17:39:51][D][wifi:319]: Found networks:
[17:39:51][I][wifi:365]: - 'XXXXXXXXXXXXXXXX' [redacted]▂▄▆█
[17:39:51][D][wifi:366]:     Channel: 5
[17:39:51][D][wifi:367]:     RSSI: -22 dB
[17:39:51][D][wifi:369]: - [redacted] [redacted]▂▄▆█
[17:39:51][I][wifi:193]: WiFi Connecting to 'XXXXXXXXXXXXXXXXXXX'...
[17:39:52][I][wifi:423]: WiFi Connected!
[17:39:52][C][wifi:283]:   SSID: [redacted]
[17:39:52][C][wifi:284]:   IP Address: 192.168.1.109
[17:39:52][C][wifi:286]:   BSSID: [redacted]
[17:39:52][C][wifi:287]:   Hostname: 'esp32_sonoff'
[17:39:52][C][wifi:291]:   Signal strength: -22 dB ▂▄▆█
[17:39:52][C][wifi:295]:   Channel: 5
[17:39:52][C][wifi:296]:   Subnet: 255.255.255.0
[17:39:52][C][wifi:297]:   Gateway: 192.168.1.1
[17:39:52][C][wifi:298]:   DNS1: 192.168.1.1
[17:39:52][C][wifi:299]:   DNS2: 192.168.1.1
[17:39:52][D][wifi:432]: Disabling AP...
[17:39:52][C][ota:029]: Over-The-Air Updates:
[17:39:52][C][ota:030]:   Address: esp32_sonoff.local:3232
[17:39:52][W][ota:036]: Last Boot was an unhandled reset, will proceed to safe mode in 7 restarts
[17:39:52][C][api:022]: Setting up Home Assistant API server...
[17:39:52][I][app:058]: setup() finished successfully!
```
Kan esp32 ikke forbinde til netwærket, så check at du fik fjernet " som vist oven over.