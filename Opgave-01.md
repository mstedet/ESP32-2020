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
    ssid: "esp32_01_sekt Fallback Hotspot"
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
ESPHome Dashboardmore_vert
/dev/ttyUSB0 (CP2102 USB to UART Bridge Controller)
memory
esp32_01_sektmore_vert
 . Full path: /config/esphome/esp32_01_sekt.yaml

UPLOAD EDIT SHOW LOGS VALIDATE
Compile And Upload esp32_01_sekt.yaml
INFO Reading configuration /config/esphome/esp32_01_sekt.yaml...
INFO Generating C++ source...
INFO Core config or version changed, cleaning build files...
INFO Compiling app...
INFO Running:  platformio run -d /config/esphome/esp32_01_sekt
Processing esp32_01_sekt (board: esp32dev; framework: arduino; platform: espressif32@1.12.1)
--------------------------------------------------------------------------------
HARDWARE: ESP32 240MHz, 320KB RAM, 4MB Flash
PACKAGES: 
 - framework-arduinoespressif32 3.10004.200129 (1.0.4) 
 - tool-esptoolpy 1.20600.0 (2.6.0) 
 - toolchain-xtensa32 2.50200.80 (5.2.0)
Looking for AsyncTCP-esphome library in registry
LibraryManager: Installing id=6798 @ 1.1.1
AsyncTCP-esphome @ 1.1.1 has been successfully installed!
Looking for ESPAsyncWebServer-esphome library in registry
LibraryManager: Installing id=6758 @ 1.2.6
ESPAsyncWebServer-esphome @ 1.2.6 has been successfully installed!
Looking for ESPAsyncTCP-esphome library in registry
LibraryManager: Installing id=6757
ESPAsyncTCP-esphome @ 1.2.3 has been successfully installed!
Looking for AsyncTCP-esphome library in registry
LibraryManager: Installing id=6798
AsyncTCP-esphome @ 1.1.1 has been successfully installed!
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
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/components/api/api_connection.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/components/api/api_pb2.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/components/api/api_pb2_service.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/components/api/api_server.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/components/api/list_entities.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/components/api/proto.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/components/api/subscribe_state.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/components/api/user_services.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/components/api/util.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/components/captive_portal/captive_portal.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/components/logger/logger.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/components/ota/ota_component.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/components/web_server_base/web_server_base.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/components/wifi/wifi_component.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/components/wifi/wifi_component_esp32.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/components/wifi/wifi_component_esp8266.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/core/application.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/core/component.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/core/controller.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/core/esphal.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/core/helpers.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/core/log.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/core/preferences.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/core/scheduler.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/esphome/core/util.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/src/main.cpp.o
Generating partitions /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/partitions.bin
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib8a4/AsyncTCP-esphome/AsyncTCP.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib789/WiFi/ETH.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib789/WiFi/WiFi.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib789/WiFi/WiFiAP.cpp.o
Archiving /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib8a4/libAsyncTCP-esphome.a
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib789/WiFi/WiFiClient.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib789/WiFi/WiFiGeneric.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib789/WiFi/WiFiMulti.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib789/WiFi/WiFiSTA.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib789/WiFi/WiFiScan.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib789/WiFi/WiFiServer.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib789/WiFi/WiFiUdp.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/libe94/ESPmDNS/ESPmDNS.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib790/FS/FS.cpp.o
Archiving /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib789/libWiFi.a
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib790/FS/vfs_api.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib226/ESPAsyncWebServer-esphome/AsyncEventSource.cpp.o
Archiving /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/libe94/libESPmDNS.a
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib226/ESPAsyncWebServer-esphome/AsyncWebSocket.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib226/ESPAsyncWebServer-esphome/SPIFFSEditor.cpp.o
Archiving /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib790/libFS.a
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib226/ESPAsyncWebServer-esphome/WebAuthentication.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib226/ESPAsyncWebServer-esphome/WebHandlers.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib226/ESPAsyncWebServer-esphome/WebRequest.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib226/ESPAsyncWebServer-esphome/WebResponses.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib226/ESPAsyncWebServer-esphome/WebServer.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib43b/DNSServer/DNSServer.cpp.o
Archiving /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib43b/libDNSServer.a
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/liba61/Update/Updater.cpp.o
Archiving /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/libFrameworkArduinoVariant.a
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/Esp.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/FunctionalInterrupt.cpp.o
Archiving /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/lib226/libESPAsyncWebServer-esphome.a
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/HardwareSerial.cpp.o
Archiving /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/liba61/libUpdate.a
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/IPAddress.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/IPv6Address.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/MD5Builder.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/Print.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/Stream.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/StreamString.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/WMath.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/WString.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/base64.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/cbuf.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/esp32-hal-adc.c.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/esp32-hal-bt.c.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/esp32-hal-cpu.c.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/esp32-hal-dac.c.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/esp32-hal-gpio.c.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/esp32-hal-i2c.c.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/esp32-hal-ledc.c.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/esp32-hal-matrix.c.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/esp32-hal-misc.c.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/esp32-hal-psram.c.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/esp32-hal-rmt.c.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/esp32-hal-sigmadelta.c.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/esp32-hal-spi.c.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/esp32-hal-time.c.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/esp32-hal-timer.c.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/esp32-hal-touch.c.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/esp32-hal-uart.c.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/libb64/cdecode.c.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/libb64/cencode.c.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/main.cpp.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/stdlib_noniso.c.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/wiring_pulse.c.o
Compiling /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/FrameworkArduino/wiring_shift.c.o
Archiving /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/libFrameworkArduino.a
Linking /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/firmware.elf
Retrieving maximum program size /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/firmware.elf
Checking size /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/firmware.elf
Building /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/firmware.bin
Advanced Memory Usage is available via "PlatformIO Home > Project Inspect"
RAM:   [=         ]  12.9% (used 42320 bytes from 327680 bytes)
Flash: [=====     ]  53.1% (used 870270 bytes from 1638400 bytes)
========================= [SUCCESS] Took 81.20 seconds =========================
INFO Successfully compiled program.
INFO Running:  platformio run -d /config/esphome/esp32_01_sekt -t upload --upload-port /dev/ttyUSB0
Processing esp32_01_sekt (board: esp32dev; framework: arduino; platform: espressif32@1.12.1)
--------------------------------------------------------------------------------
PackageManager: Installing tool-mkspiffs @ ~2.230.0
tool-mkspiffs @ 2.230.0 has been successfully installed!
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
Wrote 15872 bytes (10319 compressed) at 0x00001000 in 0.2 seconds (effective 535.8 kbit/s)...
Hash of data verified.
Compressed 3072 bytes to 143...

Writing at 0x00008000... (100 %)
Wrote 3072 bytes (143 compressed) at 0x00008000 in 0.0 seconds (effective 4881.8 kbit/s)...
Hash of data verified.
Compressed 8192 bytes to 47...

Writing at 0x0000e000... (100 %)
Wrote 8192 bytes (47 compressed) at 0x0000e000 in 0.0 seconds (effective 17578.7 kbit/s)...
Hash of data verified.
Compressed 870384 bytes to 485920...

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
Wrote 870384 bytes (485920 compressed) at 0x00010000 in 12.4 seconds (effective 563.5 kbit/s)...
Hash of data verified.

Leaving...
Hard resetting via RTS pin...
========================= [SUCCESS] Took 24.94 seconds =========================
INFO Successfully uploaded program.
INFO Starting log output from /dev/ttyUSB0 with baud rate 115200
[16:41:10][D][wifi:304]: Starting scan...
[16:41:12][D][wifi:319]: Found networks:
[16:41:12][I][wifi:365]: - 'HUAWEI-ESP32' [redacted]▂▄▆█
[16:41:12][D][wifi:366]:     Channel: 11
[16:41:12][D][wifi:367]:     RSSI: -43 dB
[16:41:12][D][wifi:369]: - [redacted] [redacted]▂▄▆█
[16:41:12][D][wifi:369]: - [redacted] [redacted]▂▄▆█
[16:41:12][D][wifi:369]: - [redacted] [redacted]▂▄▆█
[16:41:12][D][wifi:369]: - [redacted] [redacted]▂▄▆█
[16:41:12][I][wifi:193]: WiFi Connecting to 'HUAWEI-ESP32'...
[16:41:13][I][wifi:423]: WiFi Connected!
[16:41:13][C][wifi:283]:   SSID: [redacted]
[16:41:13][C][wifi:284]:   IP Address: 192.168.8.103
[16:41:13][C][wifi:286]:   BSSID: [redacted]
[16:41:13][C][wifi:287]:   Hostname: 'esp32_01_sekt'
[16:41:13][C][wifi:291]:   Signal strength: -40 dB ▂▄▆█
[16:41:13][C][wifi:295]:   Channel: 11
[16:41:13][C][wifi:296]:   Subnet: 255.255.255.0
[16:41:13][C][wifi:297]:   Gateway: 192.168.8.1
[16:41:13][C][wifi:298]:   DNS1: 192.168.8.1
[16:41:13][C][wifi:299]:   DNS2: 0.0.0.0
[16:41:13][D][wifi:432]: Disabling AP...
[16:41:13][C][ota:029]: Over-The-Air Updates:
[16:41:13][C][ota:030]:   Address: esp32_01_sekt.local:3232
[16:41:13][C][api:022]: Setting up Home Assistant API server...
[16:41:13][I][app:058]: setup() finished successfully!
[16:41:13][I][app:100]: ESPHome version 1.14.4 compiled on Sep 11 2020, 16:39:56
[16:41:13][C][wifi:415]: WiFi:
[16:41:13][C][wifi:283]:   SSID: [redacted]
[16:41:13][C][wifi:284]:   IP Address: 192.168.8.103
[16:41:13][C][wifi:286]:   BSSID: [redacted]
[16:41:13][C][wifi:287]:   Hostname: 'esp32_01_sekt'
[16:41:13][C][wifi:291]:   Signal strength: -40 dB ▂▄▆█
[16:41:13][C][wifi:295]:   Channel: 11
[16:41:13][C][wifi:296]:   Subnet: 255.255.255.0
[16:41:13][C][wifi:297]:   Gateway: 192.168.8.1
[16:41:13][C][wifi:298]:   DNS1: 192.168.8.1
[16:41:13][C][wifi:299]:   DNS2: 0.0.0.0
[16:41:13][C][logger:175]: Logger:
[16:41:13][C][logger:176]:   Level: DEBUG
[16:41:13][C][logger:177]:   Log Baud Rate: 115200
[16:41:13][C][logger:178]:   Hardware UART: UART0
[16:41:13][C][captive_portal:169]: Captive Portal:
[16:41:13][C][ota:029]: Over-The-Air Updates:
[16:41:13][C][ota:030]:   Address: esp32_01_sekt.local:3232
[16:41:13][C][api:095]: API Server:
[16:41:13][C][api:096]:   Address: esp32_01_sekt.local:6053
[16:43:10][I][ota:046]: Boot seems successful, resetting boot loop counter.
help_outline   more_vert
© 2019 Copyright ESPHome, Made with MaterializeESPHome 1.14.4 Documentation
```
Hvis alt er gået godt er vi kalr til næste opgave

