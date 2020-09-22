# Opgave-02 - Opret en Secretfil 
Gem adgangskoder og andre følsomme data ved hjælp af! Secret
Ligesom i Home Assistant-konfigurationsfiler er det muligt at bruge! Secret i ESPHome. Så i stedet for at have følsomme oplysninger spredt over forskellige konfigurationsfiler, kan du gemme dem alle ét sted.
ESPHome-dashboardet har en Secrets Editor tilgængelig, som er tilgængelig via menuikonet øverst til højre.

## Åben ESPHome's Secrets Editor
* tilføj nu disse liner til filen:
```
My_WiFi_SSID: "HUAWEI-ESP32"
My_WiFi_Pass: "12345678"
My_Access_Pass: "qazwsxedc"
My_AP_Pass: "qwertyuiop"
My_API_Pass: "asdfghjkl"
My_OTA_Pass: "zxcvbnm"
```
* Save & Close filen  

Når du tilføjer noget for første gang via tekstbehandlingen, opretter ESPHome automatisk secrets.yaml-filen inde i ESPHome-mappen i mappen Home Assistant Config.   
* Filem bliver gemt som "/config/esphome/secrets.yaml"

## Åben nu ESP32 configurationsfilen
Efter lagring af data i filen secrets.yaml. For eksempel adgangskoden til WiFi kan du derefter gå til dine ESPHome-enheder og i konfigurationsfilen erstatte adgangskoden med følgende:

### [WiFi Password](https://esphome.io/components/wifi.html#wifi-component)
* fra
```
wifi:
  ssid: "HUAWEI-ESP32"
  password: "12345678"
```
* til 
```
wifi:
  ssid: !secret My_WiFi_SSID
  password: !secret My_WiFi_Pass
```
### [AP Password](https://esphome.io/components/wifi.html#configuration-variables)
* fra
```
  ap:
    ssid: "esp32_01_sekt Fallback Hotspot"
    password: "icec5M2D12pb"
```
til
```
  ap:
    ssid: "esp32_01_sekt Fallback Hotspot"
    password: !secret My_AP_Pass
```
### [API Password](https://esphome.io/components/api.html) 
fra
```
api:
```
til
```
api:
  password: !secret My_API_Pass
```
### [OTA Password](https://esphome.io/components/ota.html)
fra
```
ota:
```
til
```
ota:
  password: !secret My_OTA_Pass
```

* Save & Close filen
Filem bliver gemt som "/config/esphome/esp32_01_sekt.yaml"




## Reprogramer din ESP32 med den nye opsætning
Efter redigering af konfigurationsfilen skal du uploade den til enheden, og den vil erstatte det! Hemmelige navn med de faktiske data, der er på filen secrets.yaml.

* Vælg den USB-port som din ESP32 er forbundet til
* Check Config, hvis ok så fortsæt med næste punkt ellers ret fejl
* Upload nu ændringer til din ESP32
* Du skal nu gerne se noget som dette:
```
ESPHome Dashboardmore_vert
/dev/ttyUSB0 (CP2102 USB to UART Bridge Controller)
memory
esp32_01_sektmore_vert
 . Full path: /config/esphome/esp32_01_sekt.yaml

UPLOAD EDIT SHOW LOGS VALIDATE
Compile And Upload esp32_01_sekt.yaml
INFO Reading configuration /config/esphome/esp32_01_sekt.yaml...
INFO Generating C++ source...
INFO Compiling app...
INFO Running:  platformio run -d /config/esphome/esp32_01_sekt
Processing esp32_01_sekt (board: esp32dev; framework: arduino; platform: espressif32@1.12.1)
--------------------------------------------------------------------------------
HARDWARE: ESP32 240MHz, 320KB RAM, 4MB Flash
PACKAGES: 
 - framework-arduinoespressif32 3.10004.200129 (1.0.4) 
 - tool-esptoolpy 1.20600.0 (2.6.0) 
 - toolchain-xtensa32 2.50200.80 (5.2.0)
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
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/main.cpp.o
Linking /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/firmware.elf
Building /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/firmware.bin
Retrieving maximum program size /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/firmware.elf
Checking size /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/firmware.elf
Advanced Memory Usage is available via "PlatformIO Home > Project Inspect"
RAM:   [=         ]  12.9% (used 42320 bytes from 327680 bytes)
Flash: [=====     ]  53.1% (used 870270 bytes from 1638400 bytes)
========================= [SUCCESS] Took 20.86 seconds =========================
INFO Successfully compiled program.
INFO Running:  platformio run -d /config/esphome/esp32_01_sekt -t upload --upload-port /dev/ttyUSB0
Processing esp32_01_sekt (board: esp32dev; framework: arduino; platform: espressif32@1.12.1)
--------------------------------------------------------------------------------
HARDWARE: ESP32 240MHz, 320KB RAM, 4MB Flash
PACKAGES: 
 - framework-arduinoespressif32 3.10004.200129 (1.0.4) 
 - tool-esptoolpy 1.20600.0 (2.6.0) 
 - tool-mkspiffs 2.230.0 (2.30) 
 - toolchain-xtensa32 2.50200.80 (5.2.0)
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
Retrieving maximum program size /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/firmware.elf
Checking size /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/firmware.elf
Advanced Memory Usage is available via "PlatformIO Home > Project Inspect"
RAM:   [=         ]  12.9% (used 42320 bytes from 327680 bytes)
Flash: [=====     ]  53.1% (used 870270 bytes from 1638400 bytes)
Configuring upload protocol...
AVAILABLE: esp-prog, espota, esptool, iot-bus-jtag, jlink, minimodule, olimex-arm-usb-ocd, olimex-arm-usb-ocd-h, olimex-arm-usb-tiny-h, olimex-jtag-tiny, tumpa
CURRENT: upload_protocol = esptool
Looking for upload port...
Use manually specified: /dev/ttyUSB0
Uploading /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/firmware.bin
Serial port /dev/ttyUSB0
Connecting........_____.
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
Wrote 15872 bytes (10319 compressed) at 0x00001000 in 0.2 seconds (effective 529.0 kbit/s)...
Hash of data verified.
Compressed 3072 bytes to 143...

Writing at 0x00008000... (100 %)
Wrote 3072 bytes (143 compressed) at 0x00008000 in 0.0 seconds (effective 3484.5 kbit/s)...
Hash of data verified.
Compressed 8192 bytes to 47...

Writing at 0x0000e000... (100 %)
Wrote 8192 bytes (47 compressed) at 0x0000e000 in 0.0 seconds (effective 11892.8 kbit/s)...
Hash of data verified.
Compressed 870384 bytes to 485914...

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
Wrote 870384 bytes (485914 compressed) at 0x00010000 in 12.2 seconds (effective 570.1 kbit/s)...
Hash of data verified.

Leaving...
Hard resetting via RTS pin...
========================= [SUCCESS] Took 26.82 seconds =========================
INFO Successfully uploaded program.
INFO Starting log output from /dev/ttyUSB0 with baud rate 115200
[18:21:31][D][wifi:304]: Starting scan...
[18:21:33][D][wifi:319]: Found networks:
[18:21:33][I][wifi:365]: - 'HUAWEI-ESP32' [redacted]▂▄▆█
[18:21:33][D][wifi:366]:     Channel: 11
[18:21:33][D][wifi:367]:     RSSI: -54 dB
[18:21:33][D][wifi:369]: - [redacted] [redacted]▂▄▆█
[18:21:33][D][wifi:369]: - [redacted] [redacted]▂▄▆█
[18:21:33][D][wifi:369]: - [redacted] [redacted]▂▄▆█
[18:21:33][D][wifi:369]: - [redacted] [redacted]▂▄▆█
[18:21:33][I][wifi:193]: WiFi Connecting to 'HUAWEI-ESP32'...
[18:21:34][I][wifi:423]: WiFi Connected!
[18:21:34][C][wifi:283]:   SSID: [redacted]
[18:21:34][C][wifi:284]:   IP Address: 192.168.8.103
[18:21:34][C][wifi:286]:   BSSID: [redacted]
[18:21:34][C][wifi:287]:   Hostname: 'esp32_01_sekt'
[18:21:34][C][wifi:291]:   Signal strength: -52 dB ▂▄▆█
[18:21:34][C][wifi:295]:   Channel: 11
[18:21:34][C][wifi:296]:   Subnet: 255.255.255.0
[18:21:34][C][wifi:297]:   Gateway: 192.168.8.1
[18:21:34][C][wifi:298]:   DNS1: 192.168.8.1
[18:21:34][C][wifi:299]:   DNS2: 0.0.0.0
[18:21:34][D][wifi:432]: Disabling AP...
[18:21:34][C][ota:029]: Over-The-Air Updates:
[18:21:34][C][ota:030]:   Address: esp32_01_sekt.local:3232
[18:21:34][C][api:022]: Setting up Home Assistant API server...
[18:21:34][I][app:058]: setup() finished successfully!
[18:21:34][I][app:100]: ESPHome version 1.14.4 compiled on Sep 11 2020, 18:20:48
[18:21:34][C][wifi:415]: WiFi:
[18:21:34][C][wifi:283]:   SSID: [redacted]
[18:21:34][C][wifi:284]:   IP Address: 192.168.8.103
[18:21:34][C][wifi:286]:   BSSID: [redacted]
[18:21:34][C][wifi:287]:   Hostname: 'esp32_01_sekt'
[18:21:34][C][wifi:291]:   Signal strength: -52 dB ▂▄▆█
[18:21:34][C][wifi:295]:   Channel: 11
[18:21:34][C][wifi:296]:   Subnet: 255.255.255.0
[18:21:34][C][wifi:297]:   Gateway: 192.168.8.1
[18:21:34][C][wifi:298]:   DNS1: 192.168.8.1
[18:21:34][C][wifi:299]:   DNS2: 0.0.0.0
[18:21:34][C][logger:175]: Logger:
[18:21:34][C][logger:176]:   Level: DEBUG
[18:21:34][C][logger:177]:   Log Baud Rate: 115200
[18:21:34][C][logger:178]:   Hardware UART: UART0
[18:21:34][C][captive_portal:169]: Captive Portal:
[18:21:34][C][ota:029]: Over-The-Air Updates:
[18:21:34][C][ota:030]:   Address: esp32_01_sekt.local:3232
[18:21:34][C][api:095]: API Server:
[18:21:34][C][api:096]:   Address: esp32_01_sekt.local:6053
help_outline   more_vert
© 2019 Copyright ESPHome, Made with MaterializeESPHome 1.14.4 Documentation
```
Hvis alt er gået godt er vi kalr til trin 03


