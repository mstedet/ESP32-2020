# ESP32_Kontakt  
## Diagram  
![ESP32-Kontakt](/Opgaver/ESP32-Kontakt/ESP32-Kontakt_bb.png) 
## Config data for oprettelse af configurationsfil
```
Device Name: esp32_kontakt_xxxx
Device Type: Espressif ESP32 Dev Module
WiFi SSID: "HUAWEI-ESP32"
WiFi Password: "12345678"
Access Password: ""
```
## !secrets fil /config/esphome/secrecs.yaml
```
My_WiFi_SSID: "HUAWEI-ESP32"
My_WiFi_Pass: "12345678"
My_Access_Pass: "qazwsxedc"
My_AP_Pass: "qwertyuiop"
My_API_Pass: "asdfghjkl"
My_OTA_Pass: "zxcvbnm"
```
## Kode / Configurationsfil /config/esphome/esp32_kontakt_sekt/
```
esphome:
  name: esp32_kontakt_sekt
  platform: ESP32
  board: esp32dev

wifi:
  ssid: !secret My_WiFi_SSID
  password: !secret My_WiFi_Pass

  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "Esp32_Kontakt Sekt"
    password: !secret My_AP_Pass

captive_portal:

# Enable logging
logger:

# Enable Home Assistant API
api:
  password: !secret My_API_Pass

ota:
  password: !secret My_OTA_Pass

binary_sensor:
  - platform: gpio
    pin:
      number: GPIO4
      mode: INPUT_PULLUP
      inverted: True
    name: "Desk light button 1"
    on_press:
      - switch.toggle: relay_1
  - platform: gpio
    pin:
      number: GPIO0
      mode: INPUT_PULLUP
      inverted: True
    name: "Desk light button 2"
    on_press:
      - switch.toggle: relay_2

switch:
  - platform: gpio
    pin: GPIO27
    name: "Desk light relay 1"
    inverted: true
    id: relay_1
  - platform: gpio
    pin: GPIO26
    name: "Desk light relay 2"
    inverted: true
    id: relay_2
  - platform: gpio
    pin: GPIO25
    name: "Desk light relay 3"
    inverted: true
    id: relay_3
  - platform: gpio
    pin: GPIO33
    name: "Desk light relay 4"
    inverted: true
    id: relay_4
  - platform: gpio
    pin: GPIO14
    name: "Red LED"
    inverted: true
    id: RedLed
  - platform: template
    name: "Desk light Template"
    optimistic: true
    id: relayandled
    turn_on_action:
    -  switch.toggle: relay_2
    -  switch.toggle: RedLed
    turn_off_action:
    -  switch.toggle: relay_2 
    -  switch.toggle: RedLed

status_led:
  pin:
    number: GPIO12
    
sensor:
  - platform: wifi_signal
    name: "Desk Light WiFi Signal"
    update_interval: 60s
  - platform: uptime
    name: "Desk Light Uptime"

text_sensor:
  - platform: version
    name: "Desk Light ESPHome version"
```
# Kilde & Inspiration:
## Opgave beskrivelse:
ESP32-Kontakt er en opgave hvor vi skal forbinde 2 tryk kontakter, 2 lysdioder (rød og grøn), og et relæprint med 4 relæer.
* Grønd lysdiode skal bruges som indikator for WiFi-forbindelse (status led)
* Trykkanp 1 skal tænde relæ 1 og rød lysdiode
* Trykkanp 2 skal tænde relæ 2
## Opgave trin
* 01 Opret grundlæggende konfigurations fil
* 02 Opret secret-fil til gemme password i, og ret konfigurations fil til at bruge filen 
* 03 Forbind Trykknapper og Lysdioder, og tilføj kode for dem
* 04 Forbind Relæ-print og tilføj og ret kode
* 05 OTA (Over_The_Air) opdateringer
* 06 Tilføj status-led, sensor for WiFi signal, ESPHome version.

Min opgave ESP32-Kontakt er stærkt Inspireret af Juan [@juanmtech ](https://twitter.com/JuanMTech) April 8, 2019, https://www.juanmtech.com/how-to-get-started-with-esphome-and-sonoff, jeg har ændret den til at bruge ESP32 som vores udviklingskort [ESP32-Seniorhus-2020-1](https://github.com/sekt1953/ESP32-Seniorhus-2020-1) er baseret på.