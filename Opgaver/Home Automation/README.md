# Opgave-01 HomeAutomation
## ESPHome Create New Node:
* Opret nu et ESPHOME Node med dette indhold, hvor XXXX skal erstattes med dine initialer.

```
esphome:
  name: XXXX_auto
  platform: ESP32
  board: esp32dev

wifi:
  networks:
  - ssid: !secret My_WiFi_SSID
    password: !secret My_WiFi_Pass
  - ssid: !secret XXXX_WiFi_SSID
    password: !secret XXXX_WiFi_Pass


  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "XXXX Auto Fallback"
    password: !secret My_AP_Pass

captive_portal:

# Enable logging
logger:

# Enable Home Assistant API
api:
  password: !secret My_API_Pass

ota:
  password: !secret My_OTA_Pass

sensor:
  - platform: wifi_signal
    name: "XXXX_auto WiFi signal"
    update_interval: 60s

  - platform: uptime
    name: "XXXX_auto uptime"

text_sensor:
  - platform: wifi_info
    ip_address:
      name: "XXXX_auto ESP IP Address"
    ssid:
      name: "XXXX_auto ESP Connected SSID"
    bssid:
      name: "XXXX_auto ESP Connected BSSID"
    mac_address:
      name: "XXXX_auto ESP Mac Wifi Address"
  - platform: version
    name: "XXXX_auto ESPHome version"

binary_sensor:
  - platform: gpio
    pin:
      number: GPIO32
      mode: INPUT_PULLUP
      inverted: True
    name: "XXXX_auto_pir_01"
  - platform: gpio
    pin:
      number: GPIO33
      mode: INPUT_PULLUP
      inverted: True
    name: "XXXX_auto_frontdoor"

switch:
- platform: gpio
    pin: GPIO25
    name: "XXXX_auto_Red LED"
    inverted: true
    id: XXXX_auto_RedLed
  - platform: gpio
    pin: GPIO26
    name: "XXXX_auto_Green LED"
    inverted: true
    id: XXXX_auto_GreenLed
```
## ESPHome Secrets Editor
* Open Opret en Secret file med dette indhold, XXXX erstatest med dine Initialer, yyyyyyyy med dit hjemmenetwærks SSID, zzzzzzzz erstattest med dit hjemmenetværks Password
```
My_WiFi_SSID: "HUAWEI-ESP32"
My_WiFi_Pass: "12345678"
My_Access_Pass: "qazwsxedc"
My_AP_Pass: "qwertyuiop"
My_API_Pass: "asdfghjkl"
My_OTA_Pass: "zxcvbnm"

XXXX_WiFi_SSID: "yyyyyyyy"
XXXX_WiFi_Pass: "zzzzzzzz"
```
