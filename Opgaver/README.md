# Link
## ESP32
* [Andresa Spiess](https://www.youtube.com/c/AndreasSpiess/playlists)
  * [Which ESP32 pins are safe to use?](https://www.youtube.com/watch?v=LY-1DHTxRAk)
    * [Excel Sheet:](https://www.youtube.com/redirect?v=LY-1DHTxRAk&event=video_description&redir_token=QUFFLUhqbDg0S3ZSNW1mSmFqSURKVy1JVHNIbmlDMzY3QXxBQ3Jtc0ttNzNkdlN0YVBKVjg2YURZNl9TR2h6SWgwbExaS0RjVTNsWnZELWFEZHVfNHRMZ2xDU25lSDZnVVdYN0xvYl8yMTZ1eG1fak1WSmFHdHNDUDg2WjNIMk5BY3dqQVFlOHJhOHByaExVTkhnZEpuRVV1NA%3D%3D&q=https%3A%2F%2Fdrive.google.com%2Ffile%2Fd%2F1gbKM7DA7PI7s1-ne_VomcjOrb0bE2TPZ%2Fview%3Fusp%3Dsharing)

## Home Automation
* [Smart Home Junkie](https://www.youtube.com/c/smarthomejunkie/playlists)
  * [How to set up Automations in Home Assistant tutorial](https://www.youtube.com/watch?v=KXTs5_x_T5c)
  * [Create a professional alarm system in Home Assistant. This is how!](https://www.youtube.com/watch?v=JPSDAszlII4&list=PLKuGrHcHLKMjYTsVN8IAKPLE21MbqkISO)
* [KPeyanski](https://www.youtube.com/channel/UCiyU6otsAn6v2NbbtM85npg)
  * [Home Assistant Android Companion App | SENSORS & NOTIFICATIONS](https://www.youtube.com/watch?v=pTa-SCWXMSQ&t=436s)
* [BeardedTinker](https://www.youtube.com/channel/UCuqokNoK8ZFNQdXxvlE129g)
  * [Home Assistant How To - track Threshold and use with sensors](https://www.youtube.com/watch?v=49Nv1HqYhqQ)

### Home Automation - Lovelace
* [Zack Barett](https://www.youtube.com/channel/UCXpteV7qpsWi9uUkOeLAhaA)
  * [Beginner's Guide on the Lovelace Dashboard Editor](https://www.youtube.com/watch?v=21dAWsKUimc)
  * [Everything Home Assistant Frontend](https://www.youtube.com/watch?v=8E3A90Xv7vA&list=PLs3GdbE8i1fRElfRyuaIRkyOsuBqYWrBA)
* [Home Sight](https://www.youtube.com/channel/UCT4bjO68FpyOsVoQAe45MGQ)
  * [Home Assistant how to create a Lovelace 3D floorplan with light overlays and buttons - Pt1](https://www.youtube.com/watch?v=xGIH6MlbRn0)
* [ Everything Smart Home](https://www.youtube.com/channel/UCrVLgIniVg6jW38uVqDRIiQ)
  * [Installing Home Assistant OS (Hassio) on Raspberry Pi and Quick Lovelace Tour/Overview](https://www.youtube.com/watch?v=SHg6fa0x7OA)
### Home Automation - Nextion Display
* [Vaclav Chaloupka](https://www.youtube.com/channel/UCA5DCnztFFHgdEettFHZ2Kw)
  * [DIY displays for Home Assistant](https://www.youtube.com/watch?v=_u1sOCfyghY)
### Home Automation - RFID
#### PN522
* [DrZzs](https://www.youtube.com/channel/UC7G4tLa4Kt6A9e3hJ-HO8ng)
  * [ID Card Scanner using NodeMCU, MFRC-522, esp-rfid firmware, and of course, Home Assistant](https://www.youtube.com/watch?v=ENMul9eAB00)
  * [esprfid/esp-rfid](https://github.com/esprfid/esp-rfid)
#### PN532
* [ESPHome](https://esphome.io/)
  * [PN532 NFC/RFID](https://esphome.io/components/binary_sensor/pn532.html)
* [BeardedTinker](https://www.youtube.com/channel/UCuqokNoK8ZFNQdXxvlE129g)
  * [Home Assistant How To - make NFC Tag Reader with PN532 & ESPHome](https://www.youtube.com/watch?v=YqwRppUsFIQ)
  * [PN532 NFC RFID module V3](https://arduinotech.dk/shop/pn532-nfc-rfid-module-v3/)
  * [ PN532 NFC/RFID-controller, Adafruit](https://www.elfadistrelec.dk/da/pn532-nfc-rfid-controller-adafruit-364/p/30129234)
### Home Automation - Push messages and notification 
* [BeardedTinker](https://www.youtube.com/channel/UCuqokNoK8ZFNQdXxvlE129g)
  * [Home Assistant How To - Push messages and notification to Telegram](https://www.youtube.com/watch?v=qskqdjUZcRY)
*  [Tobias Karge](https://www.youtube.com/channel/UCEUOShgy0beMxZl6OR6PJiA)
   *  [Telegram Nachricht mit Home Assistant (deutsch)](https://www.youtube.com/watch?v=_XI2HxTQgUQ)

# ESPHome - Default
## Config data for oprettelse af configurationsfil
```
Device Name: <Inttialer>_<ProjectNavn>_<Version>
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
## Configurationsfil /config/esphome/Inttialer_ProjectNavn_Version/
```
esphome:
  name: <Inttialer>_<ProjectNavn>_<Version>
  platform: ESP32
  board: esp32dev

wifi:
  ssid: !secret My_WiFi_SSID
  password: !secret My_WiFi_Pass

  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "[Inttialer]_[ProjectNavn]_[Version]_FallBack"
    password: !secret My_AP_Pass

captive_portal:

# Enable logging
logger:

# Enable Home Assistant API
api:
  password: !secret My_API_Pass

ota:
  password: !secret My_OTA_Pass
```

# ESP 32 Pin Layout :
![ESP32 PinLayout](/Images/ESP32S-HiLetgo_1377x724.png)  
[ESP32S-HiLetgo Dev Boad with Pinout Template](https://forum.fritzing.org/t/esp32s-hiletgo-dev-boad-with-pinout-template/5357)  

# ESP32 Priority One Pins:
| Type | GPIO   | Resaveret | Denne Node          |
| ---  | ---    | ----      | -----               |
| I/O  | GPIO04 |           | XXXX_auto_Relay_04  |
| I/O  | GPIO05 |           | XXXX_auto_Relay_01  | 
| I/O  | GPIO16 |           | XXXX_auto_Relay_03  |
| I/O  | GPIO17 |           | XXXX_auto_Relay_02  |
| I/O  | GPIO18 |           |                     |
| I/O  | GPIO19 |           |                     |
| I/O  | GPIO23 |           |                     |
| I/O  | GPIO25 |           | XXXX_auto_pir_01    |
| I/O  | GPIO26 |           | XXXX_auto_frontdoor |
| I/O  | GPIO27 |           | XXXX_DS18B20 (Data) |
| I/O  | GPIO32 |           | XXXX_auto_Red LED   |
| I/O  | GPIO33 |           | XXXX_auto_Green LED |

# ESP32 I2C Bus
| Type | GPIO   | Resaveret | 
| ---  | ---    | ----      | 
| I/O  | GPIO21 | I2C SDA   | 
| I/O  | GPIO22 | I2C SCL   | 

# ESP32 VSPI Bus
| Type | GPIO   | Resaveret | 
| ---  | ---    | ----      | 
| I/O  | GPIO23 | VSPI MOSI | 
| I/O  | GPIO19 | VSPI MISO | 
| I/O  | GPIO18 | VSPI CLK  | 
| I/O  | GPIO05 | VSPI CS   | 

# ESP32 HSPI Bus
| Type | GPIO   | Resaveret |
| ---  | ---    | ----      |
| I/O  | GPIO13 | HSPI MOSI |
| I/O  | GPIO12 | HSPI MISO |
| I/O  | GPIO14 | HSPI CLK  |
| I/O  | GPIO15 | HSPI CS   |


# ESP32 Benforbindelser:
| Type | GPIO   | True GPIO Controller    | Resaveret | 
| ---  | ---    | -----                   | ----      | 
| I/O  | GPIO00 | No                      |           | 
| I/O  | GPIO01 | No                      | TX0       | 
| I/O  | GPIO02 | No                      |           | 
| I/O  | GPIO03 | No                      | RX0       | 
| I/O  | GPIO04 |                         |           | 
| I/O  | GPIO05 |                         | VSPI CS   | 
| I/O  | GPIO12 | No                      | HSPI MISO | 
| I/O  | GPIO13 |                         | HSPI MOSI | 
| I/O  | GPIO14 |                         | HSPI CLK  | 
| I/O  | GPIO15 | No log when low         | HSPI CS   | 
| I/O  | GPIO16 | Not available on WROVER | RX2       | 
| I/O  | GPIO17 | Not available on WROVER | TX2       | 
| I/O  | GPIO18 |                         | VSPI SCK  | 
| I/O  | GPIO19 |                         | VSPI MISO | 
| I/O  | GPIO21 |                         | I2C SDA   | 
| I/O  | GPIO22 |                         | I2C SCL   | 
| I/O  | GPIO23 |                         | VSPI MOSI | 
| I/O  | GPIO25 |                         |           | 
| I/O  | GPIO26 |                         |           | 
| I/O  | GPIO27 |                         |           | 
| I/O  | GPIO32 |                         |           | 
| I/O  | GPIO33 |                         |           | 
| I    | GPIO34 | No                      |           | 
| I    | GPIO35 | No                      |           | 
| I    | GPIO36 | No                      | SENSOR_VP | 
| I    | GPIO39 | No                      | SENSOR_VN | 

# PCB Layout - TopView:
![PCB Images](/Fritzing/ESP32_PCB_A_002_b_bb.png)
