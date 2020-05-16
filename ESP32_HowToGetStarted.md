# EspHome - Sådan konfigurres en ESP32 i EspHome
Her vil jeg prøve at oprette softwaren for en "esp32_sonoff" en ESP32 som kan fjernstyre til at tænde og slukke en lamp f.eks.  
Kilde: [JuanMTech - How to get started with ESPHome and Sonoff](https://www.juanmtech.com/how-to-get-started-with-esphome-and-sonoff/)  

## 1. Edit /config/esphome/secrets.yaml
her gemmer jeg password og andre hemmeligherer jeg ikke ønsker at vise andre  
f.eks.:
```
my_ssid_id: "Dit Netværks SSID"
my_ssid_pass: "Dit Netværks password"
```

## 2. Create a configuration file
Åben ESPHome og udfyld guiden med disse oplysninger:
* Introduction And Name
  * Device Name: esp32_sonoff
* Device Type
  * Device Type: Espressif ESP32 Dev Module
* WiFi And Over-The_Air Updates
  * WiFi SSID: !secret my_ssid_id
  * WiFi Password: !secret my_ssid_pass
  * Access Password:
* Done
### Ret /config/esphome/esp32_sonoff.yaml filen:
Nu er der brug for at rette lidt i filen, når man indtaster SSDI & Password i Guiden sætter den " " omkring oplysningerne da den tror det er rigtige SSDI & Password, men jeg indsætter henvisninger så " skal fjernes.  
før:
```
wifi:
  ssid: "!secret my_ssid_id"
  password: "!secret my_ssid_pass"
```
efter:
```
wifi:
  ssid: !secret my_ssid_id
  password: !secret my_ssid_pass
```
vælg Save Close
## 3. Compile and Upload esp32_sonoff.yaml to /dev/ttyUSB0 (CP2102 USB to UART Bridge Controller):
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

## 4. Add components to the config file:

### ESP 32 Pin Layout :
![ESP32 PinLayout](/Images/ESP32S-HiLetgo_1377x724.png)  
[ESP32S-HiLetgo Dev Boad with Pinout Template](https://forum.fritzing.org/t/esp32s-hiletgo-dev-boad-with-pinout-template/5357)  

#### ESP32-DevKitC :
[ESP32-DevKitC PinOut](https://www.cloudynights.com/uploads/gallery/album_9650/gallery_16487_9650_1843894.png)  
[ESP32-DevKitC Diagram](http://esp32.net/images/Ai-Thinker/NodeMCU-32S/Ai-Thinker_NodeMCU-32S_DiagramSchematic.png)  
[ESP32_Function_Block_Diagram](http://esp32.net/images/_resources/ESP32_Function_Block_Diagram.svg)  

### Edit "esp32_sonoff.yaml" file
Nu skal der installeres configuration for LED & Relay, åben nu filen "esp32_sonoff.yaml" fra ESPHome og tilføj disse linier.

```
binary_sensor:
  - platform: gpio
    pin:
      number: GPIO0
      mode: INPUT_PULLUP
      inverted: True
    name: "Desk light button"
    on_press:
      - switch.toggle: relay

switch:
  - platform: gpio
    name: "Desk light relay"
    pin: GPIO12
    id: relay

status_led:
  pin:
    number: GPIO13
    inverted: yes

sensor:
  - platform: wifi_signal
    name: "Desk light WiFi signal"
    update_interval: 60s

  - platform: uptime
    name: "Desk light uptime"

text_sensor:
  - platform: version
    name: "Desk light ESPHome version"
```
### [ESPHome Guides, Devices, Components, Cookbook](https://esphome.io/)
* [Binary Sensor Component](https://esphome.io/components/binary_sensor/index.html)
* [Switch Component](https://esphome.io/components/switch/)
* [Status LED](https://esphome.io/components/status_led)
* [Sensor Component](https://esphome.io/components/sensor/)
  * [WiFi Signal Sensor](https://esphome.io/components/sensor/wifi_signal.html)
  * [Uptime Sensor](https://esphome.io/components/sensor/uptime.html)
  * [Version Text Sensor](https://esphome.io/components/text_sensor/index.html)
* [ESPHome Core Configuration](https://esphome.io/components/esphome.html)
  * [Configuration Types](https://esphome.io/guides/configuration-types.html)
* CPU
  * [Generic ESP8266](https://esphome.io/devices/esp8266.html)
    * [ESP8266 <BOARD_TYPE>](https://docs.platformio.org/en/latest/platforms/espressif8266.html#boards)
  * [Generic ESP32](https://esphome.io/devices/esp32.html)
    * [ESP32 <BOARD_TYPE>](https://docs.platformio.org/en/latest/platforms/espressif32.html#boards)


## 5. Forbind nu Relay, Led, Tast på vores test pcb
* Desk light button
  * Forbind "Desk light button" 1 ledning til stel (den sorte) og en gul ledning til GPIO0
  * ![Foto001.png](/Images/foto001.png)
* Desk light relay
  * Forbind "Desk light relay" jeg bruger den røde Led til at indikerer et Relay, forbind en rød ledning til +3,3V og hvid ledning til GPIO12
  * ![Foto002.png](/Images/foto002.png)
* status_led
  * Forbind "status_led" jeg bruger grøn Led som status Led, forbins rød ledning til +3,3V og en grøn ledning til GPIO13
  * ![Foto003.png](/Images/foto003.png)
* Nu er test pcb en klar til at afprøve programmet


