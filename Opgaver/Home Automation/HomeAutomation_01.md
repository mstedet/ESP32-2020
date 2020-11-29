# Opgave HomeAutomation_01
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
      number: GPIO4
      mode: INPUT_PULLUP
      inverted: True
    name: "XXXX_auto_pir_01"
  - platform: gpio
    pin:
      number: GPIO0
      mode: INPUT_PULLUP
      inverted: True
    name: "XXXX_auto_frontdoor"

switch:
- platform: gpio
    pin: GPIO14
    name: "XXXX_auto_Red LED"
    inverted: true
    id: XXXX_auto_RedLed
  - platform: gpio
    pin: GPIO12
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

## ESP32 Benforbindelser:
| Name  | Type | GPIO | True GPIO Controller | Denne Node |
| ---   | ---  | ---  | -----                | -----      |
| IO00 | I/O | GPIO00 | No |    |
| TXD0 | I/O | GPIO01 | No |    |
| IO02 | I/O | GPIO02 | No |    |
| RXD0 | I/O | GPIO03 | No |    |
| IO04 | I/O | GPIO04 |  | XXXX_auto_Relay 1 |
| IO05 | I/O | GPIO05 |  | XXXX_auto_Relay 2 |
| IO12 | I/O | GPIO12 | No |    |
| IO13 | I/O | GPIO13 |  | XXXX_auto_Relay 3 |
| IO14 | I/O | GPIO14 |  | XXXX_auto_Relay 4 |
| IO15 | I/O | GPIO15 |  |    |
| IO16 | I/O | GPIO16 | Not available on WROVER |    |
| IO17 | I/O | GPIO17 | Not available on WROVER |    |
| IO18 | I/O | GPIO18 |  |    |
| IO19 | I/O | GPIO19 |  |    |
| IO21 | I/O | GPIO21 |  |    |
| IO22 | I/O | GPIO22 |  |    |
| IO23 | I/O | GPIO23 |  |    |
| IO25 | I/O | GPIO25 |  | XXXX_auto_Red LED |
| IO26 | I/O | GPIO26 |  | XXXX_auto_Green LED |
| IO27 | I/O | GPIO27 |  |    |
| IO32 | I/O | GPIO32 |  | XXXX_auto_pir_01 |
| IO33 | I/O | GPIO33 |  | XXXX_auto_frontdoor |
| IO34 | I | GPIO34 | No |    |
| IO35 | I | GPIO35 | No |    |
| SENSOR_VP | I | GPIO36 | No |   |  
| SENSOR_VN | I | GPIO39 | No |    |