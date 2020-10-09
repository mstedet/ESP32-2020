# Raspberry Pi OS med IOTStack 

## 1. Clone IOTStack projected til din Raspberry
```
git clone https://github.com/SensorsIot/IOTstack.git ~/IOTStack
```
## 2. Start menu.sh
```
cd ~/IOTStack && bash ./menu.sh
```
### 1. Install Docker
### 2. Build Stack
#### 1. vælg Container
* Portainer
* Node-RED
* InfluxDB
* Grafana
* Eclipse-Mosquitto
* MariaDB
* Motioneye
* Next Cloud
### 3. Install Hass.io
Installer lidt programmer før installationen af Hassio
```
sudo apt install network-manager apparmor
```