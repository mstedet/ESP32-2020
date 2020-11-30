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
| Type | GPIO   | True GPIO Controller    | Resaveret | Denne Node          |
| ---  | ---    | -----                   | ----      | -----               |
| I/O  | GPIO00 | No                      |           |                     |
| I/O  | GPIO01 | No                      | TX0       |                     |
| I/O  | GPIO02 | No                      |           |                     |
| I/O  | GPIO03 | No                      | RX0       |                     |
| I/O  | GPIO04 |                         |           |                     |
| I/O  | GPIO05 |                         | VSPI SS   |                     |
| I/O  | GPIO12 | No                      |           |                     |
| I/O  | GPIO13 |                         |           |                     |
| I/O  | GPIO14 |                         |           | XXXX_auto_Relay 1   |
| I/O  | GPIO15 |                         |           | XXXX_auto_Relay 2   |
| I/O  | GPIO16 | Not available on WROVER | RX2       | XXXX_auto_Relay 3   |
| I/O  | GPIO17 | Not available on WROVER | TX2       | XXXX_auto_Relay 4   |
| I/O  | GPIO18 |                         | VSPI SCK  |                     |
| I/O  | GPIO19 |                         | VSPI MISO |                     |
| I/O  | GPIO21 |                         | I2C SDA   |                     |
| I/O  | GPIO22 |                         | I2C SCL   |                     |
| I/O  | GPIO23 |                         | VSPI MOSI |                     |
| I/O  | GPIO25 |                         |           | XXXX_auto_Red LED   |
| I/O  | GPIO26 |                         |           | XXXX_auto_Green LED |
| I/O  | GPIO27 |                         |           |                     |
| I/O  | GPIO32 |                         |           | XXXX_auto_pir_01    |
| I/O  | GPIO33 |                         |           | XXXX_auto_frontdoor |
| I    | GPIO34 | No                      |           |                     |
| I    | GPIO35 | No                      |           |                     |
| I    | GPIO36 | No                      | SENSOR_VP |                     |
| I    | GPIO39 | No                      | SENSOR_VN |                     |

