# Raspberry Pi OS med IOTStack 

Installer lidt programmer før installationen af Hassio
```
sudo apt install network-manager apparmor-utils
```

## 1. Clone IOTStack projected til din Raspberry
```
git clone https://github.com/SensorsIot/IOTstack.git ~/IOTStack
```
## 2. Start menu.sh
```
cd ~/IOTStack && bash ./menu.sh
```
### 1. Install Docker
reboot når du bliver spurt

### 2. Build Stack

#### 1. vælg Container
* Portainer
### 3. Install Hass.io
installer nu Homeasssistent fra IOTstack

## Start IOTstack
``` 
cd ~/IOTStack && docker-compose up -d
``` 