# ESP32-Kontakt  
## Diagram  
![ESP32-Kontakt](/Opgaver/ESP32-Kontakt/ESP32-Kontakt_bb.png) 
## Kode
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
    ssid: "Esp32-Kontakt Sekt"
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
    pin: GPIO14
    name: "Red LED"
    inverted: true
    id: RedLed
  - platform: template
    name: "template test"
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
## !secrets
```
My_WiFi_SSID: "HUAWEI-ESP32"
My_WiFi_Pass: "12345678"
My_Access_Pass: "qazwsxedc"
My_AP_Pass: "qwertyuiop"
My_API_Pass: "asdfghjkl"
My_OTA_Pass: "zxcvbnm"
```
## Kilde & inspiration:
Min opgave ESP32-Kontakt er stærkt Inspireret af Juan [@juanmtech ](https://twitter.com/JuanMTech) April 8, 2019, https://www.juanmtech.com/how-to-get-started-with-esphome-and-sonoff, jeg har ændret den til at bruge ESP32 som vores udviklingskort [ESP32-Seniorhus-2020-1](https://github.com/sekt1953/ESP32-Seniorhus-2020-1) er baseret på.