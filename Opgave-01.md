# Opgave-01 - Opret en ESP32 configurationsfil
## Forbind dit ESP32 Kort som vist på billederne  
![Opgaver-01_bb.png](/Images/Opgaver-01_bb.png)  
![Opgaver-01_schem.png](/Images/Opgaver-01_schem.png)  
### Ledninger tilsluttes som følger:
1. De hvide stifter ved LED forbindes til sorte stifter ved ESP32 (stel)
2. Den røde stift forbindes til ESP32 GPIO-12 
3. Den grønne stift forbindes til ESP32 GPIO-13
4. En hvide stift fra trykknap forbindes til sorte stifter ved ESP32 (stel)
5. En hvid stift fra trykknap forbindes til ESP32 GPIO-2

## Start ESPHome
Opret en configuration file erstat xxxx med dine initialer:
```
Device Name: esp32_01_xxxx
Device Type: Espressif ESP32 Dev Module
WiFi SSID: "HUAWEI-ESP32"
WiFi Password: "12345678"
Access Password: ""
```
Resultatet bliver gemt i filen "/config/esphome/esp32-01-xxxx.yaml"

## Åben nu ESPHome's' Editor
du skal nu se en fil med indhold som dette:
```
esphome:
  name: esp32_01_xxxx
  platform: ESP32
  board: esp32dev

wifi:
  ssid: "HUAWEI-ESP32"
  password: "12345678"

  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "esp32_01_xxxx Fallback Hotspot"
    password: "icec5M2D12pb"

captive_portal:

# Enable logging
logger:

# Enable Home Assistant API
api:

ota:
```
## Forbind din ESP32 til en USB-port på din HomeAssistant
* Restart ESPHome
## Programering af ESP32
* Vælg den USB-port som din ESP32 er forbundet til  
* Check Config, hvis ok så fortsæt med næste punkt ellers ret fejl
* Upload nu programmet til din ESP32
* Du skal nu gerne se noget som dette:

```
Compile and Upload esp32_sonoff.yaml to /dev/ttyUSB0 (CP2102 USB to UART Bridge Controller):

INFO Reading configuration /config/esphome/esp32_sonoff.yaml...
INFO Generating C++ source...
INFO Compiling app...
INFO Running:  platformio run -d /config/esphome/esp32_sonoff
Processing esp32_sonoff (board: esp32dev; framework: arduino; platform: espressif32@1.11.0)

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
[17:39:51][I][wifi:365]: - '4G Wi-Fi 3Danmark-8AE3' [redacted]▂▄▆█
[17:39:51][D][wifi:366]:     Channel: 5
[17:39:51][D][wifi:367]:     RSSI: -22 dB
[17:39:51][D][wifi:369]: - [redacted] [redacted]▂▄▆█
[17:39:51][I][wifi:193]: WiFi Connecting to '4G Wi-Fi 3Danmark-8AE3'...
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

Hvis alt er gået godt er vi kalr til næste opgave

