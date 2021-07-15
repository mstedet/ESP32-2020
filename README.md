# ESP32-2020
ESP32 programerings kursus 2020


## Video list
### ESP32
* [The best input and output pins on the NodeMCU ESP32 and ESP8266](https://www.youtube.com/watch?v=c0tMGlJVmkw)
### ESP32 CAM
* [Editing Camera Web Server HTML Source Code for the ESP32-CAM](https://www.youtube.com/watch?v=bIJoVyjTf7g)
  * [Code and decode html](https://gchq.github.io/CyberChef/)
* [ESP32-CAM Take Photo and Save to MicroSD Card](https://www.youtube.com/watch?v=eot6COwCPF0)
* [Sådan opsættes og bruges ESP32 WiFi-kamera](https://www.youtube.com/watch?v=5XCb3t8J4Kg&t=293s)
* [$10 DIY Wireless IP Security Camera for 3D Printers & Home](https://www.youtube.com/watch?v=6qiH1BRwUeA)
### Home Automation
* [Home Assistant: ](https://www.home-assistant.io/)
* [Home Assistant Beginners Guide: Installation, Addons, Integrations, Scripts, Scenes, and Automations](https://www.youtube.com/watch?v=sVqyDtEjudk)  
* [Home Automation With Home Assistant and ESPHome](https://www.youtube.com/watch?v=xDbH-xPQtXU)

#### The Home Assistant Beginner’s Guide
* [Install Home Assistant](https://www.home-assistant.io/getting-started/)
* [The Home Assistant Beginner’s Guide Part 1: Setting up Hass.io](https://home-assistant-guide.com/2018/04/05/the-home-assistant-beginners-guide-part-1-setting-up-hass-io/)
* [The Home Assistant Beginner’s Guide Part 2: Web Access](https://home-assistant-guide.com/2018/05/24/the-home-assistant-beginners-guide-part-2-web-access/)
* [The Home Assistant Beginner’s Guide Part 3: Integrating Home Assistant with the Google Assistant/Google Home](https://home-assistant-guide.com/2018/05/24/the-home-assistant-beginners-guide-part-3-integrating-home-assistant-with-the-google-assistant-google-home/)

#### Home Automation With Home Assistant and ESPHome
* [Home Automation With Home Assistant and ESPHome - First Steps](https://www.youtube.com/watch?v=xDbH-xPQtXU)
  * [ESPHome](https://esphome.io/)
##### [Average Automation](https://www.youtube.com/channel/UCMR_eJdL5P6SVJ2n0kTCjlg/videos)
* [Home Assistant 101 Installing](https://www.youtube.com/watch?v=9-s8379D5vg)
* [Home assistant 102 Add-ons](https://www.youtube.com/watch?v=iNNkmFJJ6Hk)
* [Home assistant 103 ESPhome custom Relays and Temperature](https://www.youtube.com/watch?v=s3Dvl8wLPSw&list=PLyxwEDtrc_EU_AsqiN2cBUJvrhFeOGAUI&index=2)
* [Home assistant 104 ESPHome Multi sensor](https://www.youtube.com/watch?v=7RpgxiIjulw)
* DrZzs
  * [ID Card Scanner using NodeMCU, MFRC-522, esp-rfid firmware, and of course, Home Assistant](https://www.youtube.com/watch?v=ENMul9eAB00&t=2s)
  * [Get Months of Battery Life from an ESP8266!](https://www.youtube.com/watch?v=1vs86fwEdtM) 
* RC522 Arduino
  * [HausnerR / esphome-door-lock](https://github.com/HausnerR/esphome-door-lock)

  
##### IHC Controller
* [IHC Controller integration for Home Assistant](https://www.home-assistant.io/integrations/ihc/)
### YAML-filer
* [YAML | In One Video](https://www.youtube.com/watch?v=cdLNKUoMc6c&t=321s)


# Argon One M.2 - Home Assistant OS: 6.x & Supervised version
## Inspiration: 
* https://community.home-assistant.io/t/raspberry-pi-4-home-assistant-os-5-5-dev-version-on-a-ssd-and-the-argon-one-m-2-case-in-progress/248025

## RPi 4b 4-8 GB Ram with M.2 SATA III boot:
### HardWare:
* Argon One M.2 V.20
* Raspberry Pi 4, 4-8GB Ram
* Verbatim, 256GB Vi560 Sata III, M.2 2280 Internal SSD, Part No. 49362
* SanDisk Ultra 16GB MicroSD-HC
* some kind of monitor with HDMI connectors maybe a TV for installation
### SoftWare:
* Raspberry Pi OS (32-bit), released: 2021-05-07
* pieeprom-2021-04-29.bin
* haos_rpi4-64-6.1 eller nyere
* unxz
## Boot with Raspberry Pi OS (32-bit) from SD-Card:
* disconnect the built-in M.2-SATA
* boot from SD-Card 16GB with Raspberry Pi OS (32-bit), released: 2021-05-07
## Install Update:
```
sudo apt update && sudo apt full-upgrade
sudo apt-get install xz-utils
```
## Update RPi Firmware, Latest for now "pieeprom-2021-04-29.bin":
```
sudo nano /etc/default/rpi-eeprom-update

sudo rpi-eeprom-update -d -f /lib/firmware/raspberrypi/bootloader/stable/pieeprom-2021-04-29.bin
```
## Set boot options:
* Connect the built-in M.2-SATA !!!
  * using the litle usd connector
* Run Raspberry config
```
sudo raspi-config
```
* …then Boot options --> Boot Rom Version --> latest -> Ok -->
  * when the system asks to “Reset boot ROM to defaults” select No (!!!) to use the latest boot ROM.
* –> Boot Order --> USB Boot --> Ok --> Finish --> Reboot --> Shut down

## Install Home Assistant OS Release 6 - (haos_rpi4):
  * Home Assistant OS Release kan be found here:  
  https://github.com/home-assistant/operating-system/releases/
```
wget https://github.com/home-assistant/operating-system/releases/download/6.1/haos_rpi4-64-6.1.img.xz

unxz haos_rpi4-64-6.1.img.xz
```
## List block devices and dd - convert and copy a file:
```
lsblk
```
* i expect M.2 SATA named **/dev/sda**
```
sudo dd bs=4M if=haos_rpi4-64-6.1.img of=/dev/sda status=progress conv=fsync
```
## Reboot:
* If all went well it will boot Home Assistant fron SSD:
  * It will take abot 5-10 min before you can get conection to **http://homeassistant.local:8123**
```
reboot
```
## ENABLE I2C VIA HOME ASSISTANT OPERATING SYSTEM TERMINAL:
I what to enable i2c to bee able to controll fan speed i the Argon40 and react to the push button on the backside of Argon40
### inspiration: 
* [ENABLE I2C VIA HOME ASSISTANT OPERATING SYSTEM TERMINAL](https://www.home-assistant.io/common-tasks/os#enable-i2c-via-home-assistant-operating-system-terminal)
* [Argon40Tech/Argon-ONE-i2c-Codes](https://github.com/Argon40Tech/Argon-ONE-i2c-Codes)
* [Misiu/argon40](https://github.com/Misiu/argon40)
* * [HassOS I2C Configurator](https://community.home-assistant.io/t/add-on-hassos-i2c-configurator/264167)

You can enable i2c via this Raspberry Pi Console:

* Login as root.
  * Type login and press enter to access the shell.
* Type the following to enable i2c, you may need to replace sda1 with sdb1 or mmcblk0p1 depending on your platform:
```
mkdir /tmp/mnt
mount /dev/sda1 /tmp/mnt
mkdir -p /tmp/mnt/CONFIG/modules
echo -ne i2c-dev>/tmp/mnt/CONFIG/modules/rpi-i2c.conf
vi /tmp/mnt/config.txt
```
find the line in config.txt
```
#dtparam=i2c_arm=on
```
and change it to this
```
dtparam=i2c_arm=on
```
Save and exit vi with thise command:  
[ESC]:w  
[ESC]:x
```
sync
reboot
```
# Add on's you will nead on your system:
## File editor 
* Configuration:
  * Option: dirsfirst (required): This option allows you to list directories before files in the file browser tree. Set it to true to list directories first, false otherwise.
  * Option: enforce_basepath (required): If set to true, access is limited to files within the /config directory.
```
dirsfirst: true
enforce_basepath: true
git: true
ignore_pattern:
  - __pycache__
  - .cloud
  - .storage
  - deps
ssh_keys: []
``` 
## ESPHome:
* Nyhere 20210616 [Power up your ESP-based projects](https://www.youtube.com/watch?v=du38Oir_xp8)
  * We're launching new tools to make it easier for new users to start with any projects running on the ESP8266 and ESP32. [Blog version:](https://www.home-assistant.io/blog/2021/06/16/power-up-your-esp-projects/)
  * [This is SO Much Better! Getting Started with ESPHome 2021](https://www.youtube.com/watch?v=iufph4dF3YU)
## Samba share:
* Configuration:
  * Option: workgroup (required): Change WORKGROUP to reflect your network needs.
  * Option: username (required): The username you would like to use to authenticate with the Samba server.
  * Option: password (required): The password that goes with the username configured for authentication.
  * Option: allow_hosts (required): List of hosts/networks allowed to access the shared folders.
```
workgroup: WORKGROUP
username: homeassistant
password: Gjq9e7UepXn6RJbc
interface: ''
allow_hosts:
  - 10.0.0.0/8
  - 172.16.0.0/12
  - 192.168.0.0/16
  - fe80::/10
veto_files:
  - ._*
  - .DS_Store
  - Thumbs.db
  - icon?
  - .Trashes
compatibility_mode: false
```
### Access Your Samba share from Linux  
* Vælg Andre steder --> Forbind til server -->
* Udfyld felt: smb://homeassistant@homeassistant.local/config --> Klik Tilslut -->
* indtast password når du bliver spurgt
  
## MariaDB 
* Start med at se denne video [Home Assistant MariaDB Install and System Monitoring](https://www.youtube.com/watch?v=FbFyqQ3He7M) fra [Everything Smart Home](https://www.youtube.com/channel/UCrVLgIniVg6jW38uVqDRIiQ)
* Configuration
  * Option: databases (required):Database name, e.g., homeassistant. Multiple are allowed.
  * Option: logins (required): This section defines a create user definition in MariaDB. Create User documentation.
    * Option: logins.username (required): Database user login, e.g., homeassistant. User Name documentation.
    * Option: logins.password (required): Password for user login. This should be strong and unique.
  * Option: rights (required):This section grant privileges to users in MariaDB. Grant documentation.
    * Option: rights.username (required):This should be the same user name defined in logins -> username.
    * Option: rights.database (required): This should be the same database defined in databases.
```
databases:
  - homeassistant
logins:
  - username: homeassistant
    password: z8wvgwg3thwhqnqy
rights:
  - username: homeassistant
    database: homeassistant  
```
### /config/configuration.yaml
```
# Home Assistant MariaDB Install and System Monitoring https://www.youtube.com/watch?v=FbFyqQ3He7M
recorder:
  db_url: !secret maria_db
```
### /config/secrets.yaml
  * for ikke at have vores password i configuration.yaml, hvor vi nemt kan komme til at dele dem med andre opretter dette entry i /config/secrets.yaml
```
# MariaDB
maria_db: mysql://homeassistant:lsjqg8ha@core-mariadb/homeassistant?charset=utf8mb4
```
## System Monitoring
### /config/configuration.yaml
```
# Sensor
sensor:
    # Home Assistant MariaDB Install and System Monitoring https://www.youtube.com/watch?v=FbFyqQ3He7M
  - platform: systemmonitor
    resources:
      - type: processor_use
      - type: processor_temperature
      - type: memory_free
      - type: disk_use_percent
        arg: /
      - type: disk_use
      - type: disk_free
      - type: throughput_network_in
        arg: eth0
      - type: throughput_network_out
        arg: eth0
```
### System Monitoring Lovelace
```
type: grid
cards:
  - type: glance
    entities:
      - entity: sensor.processor_temperature
      - entity: sensor.processor_use_percent
      - entity: sensor.memory_free
    title: Processor sensor
    state_color: false
  - type: history-graph
    entities:
      - entity: sensor.processor_temperature
      - entity: sensor.processor_use_percent
      - entity: sensor.memory_free
    hours_to_show: 48
    refresh_interval: 0
    title: Processor sensor last 48 hour
columns: 1
square: false
```
```
type: grid
cards:
  - type: entities
    entities:
      - entity: sensor.disk_use_percent
      - entity: sensor.disk_use
      - entity: sensor.disk_free
    title: Disk
  - type: entities
    entities:
      - entity: sensor.network_throughput_in_eth0
      - entity: sensor.network_throughput_out_eth0
    title: Network trafic last 48 hour
  - type: history-graph
    entities:
      - entity: sensor.network_throughput_in_eth0
      - entity: sensor.network_throughput_out_eth0
    hours_to_show: 24
    refresh_interval: 0
columns: 1
square: false
```
## SSH
* Start med at se denne video [Enable SSH In Home Assistant - TUTORIAL 2021](https://www.youtube.com/watch?v=_ANmn9QSLtA) af [Smart Home Junkie](https://www.youtube.com/channel/UCVtQ4AOSmCFUuvixddYiSxw)

### Configuration
```
log_level: info  
ssh:  
  username: homeassistant  
  password: ""  
  authorized_keys:  
    - ssh-rsa AASDJKJKJFWJFAFLCNALCMLAK234234.....  
  sftp: false  
  compatibility_mode: false  
  allow_agent_forwarding: false  
  allow_remote_port_forwarding: false  
  allow_tcp_forwarding: false  
zsh: true  
share_sessions: true  
packages:  
  - build-base  
init_commands:  
  - ls -la  
```
## Misiu/argon40:
### Misiu way of installing 
* follow this link: https://github.com/Misiu/argon40
### Automations script for Argon40:
#### Part of my configuration.yaml:
the sensor I used for getting temperature data
```
sensor:
    # Home Assistant MariaDB Install and System Monitoring https://www.youtube.com/watch?v=FbFyqQ3He7M
  - platform: systemmonitor
    resources:
      - type: processor_temperature
```
#### Helper in use:
I used the helper "Cpu_Fan_Speed" to store FanSpeed in, and to to display FanSpeed in Lovelace.
* Cpu_Fan_Speed
  * Name: Cpu_Fan_Speed
  * Icon: mdi:fan
  * Minimum value: 0
  * Maximum value: 100
  * Display mode: Input field
  * Display mode: 1
  * Entity ID: input_number.cpu_fan_speed
#### Automation - Fan_Speed_Setting:
```
alias: Fan_Speed_Setting
description: ''
trigger:
  - platform: homeassistant
    event: start
  - platform: numeric_state
    entity_id: sensor.processor_temperature
    for: '00:00:03'
    below: '30.1'
  - platform: numeric_state
    entity_id: sensor.processor_temperature
    above: '30.0'
    below: '40.1'
    for: '00:00:03'
  - platform: numeric_state
    entity_id: sensor.processor_temperature
    above: '40.0'
    below: '50.1'
    for: '00:00:03'
  - platform: numeric_state
    entity_id: sensor.processor_temperature
    above: '50.0'
    for: '00:00:03'
condition: []
action:
  - choose:
      - conditions:
          - condition: numeric_state
            entity_id: sensor.processor_temperature
            below: '30.1'
        sequence:
          - service: input_number.set_value
            target:
              entity_id: input_number.cpu_fan_speed
            data:
              value: 0
      - conditions:
          - condition: numeric_state
            entity_id: sensor.processor_temperature
            above: '30.0'
            below: '40.1'
        sequence:
          - service: input_number.set_value
            target:
              entity_id: input_number.cpu_fan_speed
            data:
              value: 10
      - conditions:
          - condition: numeric_state
            entity_id: sensor.processor_temperature
            above: '40.0'
            below: '50.1'
        sequence:
          - service: input_number.set_value
            target:
              entity_id: input_number.cpu_fan_speed
            data:
              value: 50
      - conditions:
          - condition: numeric_state
            entity_id: sensor.processor_temperature
            above: '50.0'
        sequence:
          - service: input_number.set_value
            target:
              entity_id: input_number.cpu_fan_speed
            data:
              value: 100
    default:
      - service: input_number.set_value
        target:
          entity_id: input_number.cpu_fan_speed
        data:
          value: 55
  - service: argon40.set_fan_speed
    data:
      speed: '{{ states(''input_number.cpu_fan_speed'') | int }}'
mode: single
```
### Lovelace Fan_Speed:
```
type: grid
cards:
  - type: entities
    entities:
      - entity: sensor.processor_temperature
      - entity: input_number.cpu_fan_speed
columns: 1
square: false
```
Lovelace Fan_Speed Temperature & Speed Graph:
```
type: grid
cards:
  - type: history-graph
    entities:
      - entity: sensor.processor_temperature
      - entity: input_number.cpu_fan_speed
    hours_to_show: 3
    refresh_interval: 0
    title: Processor sensor last 3 hour
columns: 1
square: false
```