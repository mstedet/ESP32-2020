# ESP32-Kontakt-03-Føj_komponenter_ til_konfigurationsfilen

OK, Du har nu oprettede konfigurationsfilen til ESP32-kontakten. Det har dog kun nogle grundlæggende indstillinger. Din software vil bare oprette forbindelse til din WiFi og intet andet. 
Så du bliver nødt til at redigere konfigurationsfilen og tilføje et par flere komponenter. For eksempel styre relæet ved at trykke på ESP32-kontakten.

## Forbind dit ESP32 Kort som vist på billederne  
Forbinder du nu de 2 LED og trykknappen til din ESP32, kan vi bruge den røde Led til at simulere et relæ og den grønne til at vise forbindelse status med og bruge trykknappen som tænd og sluk kanp.

![Opgaver-01_bb.png](/Images/ESP32-kontakten_bb.png) 

### Ledninger tilsluttes som følger:
1. De hvide stifter ved LED forbindes til sorte stifter ved ESP32 (stel)
2. Den røde stift forbindes til ESP32 GPIO12 
3. Den grønne stift forbindes til ESP32 GPIO13
4. En hvide stift fra trykknap forbindes til sorte stifter ved ESP32 (stel)
5. En hvid stift fra trykknap forbindes til ESP32 GPIO0

## Tilføj komponenter til konfigurationsfilen
Lad os gennemgå nogle af de tilgængelige indstillinger, som du kan tilføje.  
Klik på **[EDIT]** for at åbne konfigurationsfilen og indtaste følgende **nederst i filen**:
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
* binary_sensor: Udføres hvergang ESP32-kontakten bliver påvirket 
* switch: Vil skifte relæet (Rød LED) til og fra
* status_led: Nyttigt til at vise status for en enhed. Fortæller dig om advarsler eller fejl
* wifi_signal sensor: Overvåger den modtagne signalstyrke
* uptime sensor: Sporer den tid (i sekunder), enheden har været online
* version text_sensor: Giver oplysninger om den aktuelle version af ESPHome-firmwaren, der er installeret på enheden.

### Save & Close filen  
Filem bliver gemt som "/config/esphome/esp32_01_sekt.yaml"

## Reprogramer din ESP32 med den nye opsætning
* Vælg den OTA (Over-The-Air)
* Check Config, hvis ok så fortsæt med næste punkt ellers ret fejl
* Upload nu ændringer til din ESP32 via OTA
* Du skal nu gerne se noget som dette:
```
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
RAM:   [=         ]  13.0% (used 42536 bytes from 327680 bytes)
Flash: [=====     ]  55.0% (used 901062 bytes from 1638400 bytes)
========================= [SUCCESS] Took 24.87 seconds =========================
INFO Successfully compiled program.
INFO Resolving IP address of esp32_01_sekt.local
INFO  -> 192.168.8.103
INFO Uploading /data/esp32_01_sekt/.pioenvs/esp32_01_sekt/firmware.bin (901184 bytes)
Uploading: [============================================================] 100% Done...

INFO Waiting for result...
INFO OTA successful
INFO Successfully uploaded program.
INFO Starting log output from esp32_01_sekt.local using esphome API
WARNING Error resolving IP address of esp32_01_sekt.local. Is it connected to WiFi?
WARNING (If this error persists, please set a static IP address: https://esphome.io/components/wifi.html#manual-ips)
WARNING Initial connection failed. The ESP might not be connected to WiFi yet (Error resolving IP address: Error resolving address with mDNS: Did not respond. Maybe the device is offline., [Errno -5] No address associated with hostname). Re-Trying in 1 seconds
INFO Connecting to esp32_01_sekt.local:6053 (192.168.8.103)
INFO Successfully connected to esp32_01_sekt.local
[10:52:14][I][app:100]: ESPHome version 1.14.4 compiled on Sep 12 2020, 10:51:29
[10:52:14][C][status_led:019]: Status LED:
[10:52:14][C][status_led:020]:   Pin: GPIO13 (Mode: OUTPUT, INVERTED)
[10:52:14][C][wifi:415]: WiFi:
[10:52:14][C][wifi:283]:   SSID: [redacted]
[10:52:14][C][wifi:284]:   IP Address: 192.168.8.103
[10:52:14][C][wifi:286]:   BSSID: [redacted]
[10:52:14][C][wifi:287]:   Hostname: 'esp32_01_sekt'
[10:52:14][C][wifi:291]:   Signal strength: -40 dB ▂▄▆█
[10:52:14][C][wifi:295]:   Channel: 7
[10:52:14][C][wifi:296]:   Subnet: 255.255.255.0
[10:52:14][C][wifi:297]:   Gateway: 192.168.8.1
[10:52:14][C][wifi:298]:   DNS1: 192.168.8.1
[10:52:14][C][wifi:299]:   DNS2: 0.0.0.0
[10:52:14][C][gpio.binary_sensor:015]: GPIO Binary Sensor 'Desk light button'
[10:52:14][C][gpio.binary_sensor:016]:   Pin: GPIO0 (Mode: INPUT_PULLUP, INVERTED)
[10:52:14][C][switch.gpio:042]: GPIO Switch 'Desk light relay'
[10:52:14][C][switch.gpio:043]:   Pin: GPIO12 (Mode: OUTPUT)
[10:52:14][C][switch.gpio:059]:   Restore Mode: Restore (Defaults to OFF)
[10:52:14][C][uptime.sensor:030]: Uptime Sensor 'Desk light uptime'
[10:52:14][C][uptime.sensor:030]:   Unit of Measurement: 's'
[10:52:14][C][uptime.sensor:030]:   Accuracy Decimals: 0
[10:52:14][C][uptime.sensor:030]:   Icon: 'mdi:timer'
[10:52:14][C][logger:175]: Logger:
[10:52:14][C][logger:176]:   Level: DEBUG
[10:52:14][C][logger:177]:   Log Baud Rate: 115200
[10:52:14][C][logger:178]:   Hardware UART: UART0
[10:52:14][C][version.text_sensor:015]: Version Text Sensor 'Desk light ESPHome version'
[10:52:14][C][version.text_sensor:015]:   Icon: 'mdi:new-box'
[10:52:14][C][captive_portal:169]: Captive Portal:
[10:52:14][C][ota:029]: Over-The-Air Updates:
[10:52:14][C][ota:030]:   Address: esp32_01_sekt.local:3232
[10:52:14][C][api:095]: API Server:
[10:52:14][C][api:096]:   Address: esp32_01_sekt.local:6053
[10:52:14][C][wifi_signal.sensor:009]: WiFi Signal 'Desk light WiFi signal'
[10:52:14][C][wifi_signal.sensor:009]:   Unit of Measurement: 'dB'
[10:52:14][C][wifi_signal.sensor:009]:   Accuracy Decimals: 0
[10:52:14][C][wifi_signal.sensor:009]:   Icon: 'mdi:wifi'
```
## Hvis alt er gået godt er vi kalr til næste opgave
