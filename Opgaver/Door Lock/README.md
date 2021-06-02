# ESP Door Lock
## ESP8266, NODEMCU V2
## Kilde:
* [落落旅行趣](https://blog.csv.tw/2020/09/ha-esphome-rc522.html)
* [esphome-door-lock](https://github.com/HausnerR/esphome-door-lock)
* [esp-rfid](https://github.com/esprfid/esp-rfid)

```
esphome:
  name: door_lock
  platform: ESP8266
  board: nodemcuv2

wifi:
  ssid: !secret SEKT_WiFi_SSID
  password: !secret SEKT_WiFi_Pass
  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "Door Lock Fallback Hotspot"
    password: !secret SEKT_AP_Pass

captive_portal:

# Enable logging
logger:

# Enable Home Assistant API
api:
  password: !secret SEKT_API_Pass
  
ota:
  password: !secret SEKT_OTA_Pass
```
