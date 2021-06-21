# Vejledninger til HomeAssistant 2021

## Home Assistant Raspberry Pi 4 SSD Installation
* Start med at se denne video [Home Assistant Raspberry Pi 4 SSD Installation and Migration](https://www.youtube.com/watch?v=QxtDyMbDOh4) fra [Everything Smart Home](https://www.youtube.com/channel/UCrVLgIniVg6jW38uVqDRIiQ)
### Hardware ibrug i denne installation
* 1 Raspberry Pi 4 Model B 4GB
* 1 stk SSD Disk Kingston 240GB
* 1 stk SATA til USB3 Controler DELTACO USB3-SATA6G3
* 1 stk SD-Kort 8GB
* 1 stk ZigBee CC2531 USB dongle
## Min Arbejdsplads
* 1 stk PC med Ubuntu 18.04 eller nyere
### Software til brug for installationen
* link til [Secure Password Generator](https://passwordsgenerator.net/)
* hvis du ikke har en Github account skal du oprette en.
* Raspberry Pi Imager  v1.6.2 eller nyere
  * har du en tidligere versionafinstaller gammel version med komandoen:
```
sudo apt remove rpi-imager
```
og installer nyeste version med kommandoen
```
sudo snap install rpi-imager
```
### Klargør din SSD disk for Home Assistant, jeg bruger en JMicron Tech UB til ATA adapter og tilslutter min SSD via USB3 på min PC.
* CHOOSE OS: --> Other specific purpose OS -->
  * Select: Home Assistant --> Home Assistant OS 5.13 (RPI4/400)
* CHOOSE STORAGE: -->> JMicron Tech 
* WRITE: --> YES

### Klargør SD-Kort til at sætte Rasperry PI til Boote fra USD-Drev, jeg bruger et 8.0GB SD-Kort
* CHOOSE OS: --> Misc utility Images --> 
  * Select: Bootloader --> USB Boot
* CHOOSE STORAGE: -->> Generic STORAGE_DEVICE - 8.0GB
* WRITE: --> YES

# HomeAssistant på din Raspberry Pi 4
## Fra Add-on Store installerer vi nu følgende programmer 
* File editor
* Samba share
* ESPHome
* SSH
* MariaDB 
* HACS [Home Assistant Community Store](https://hacs.xyz/)
* ZigBee
* Telegram
* MQTT
* NodeRed
* AppDaemon 4 [Welcome to AppDaemon’s documentation!](https://appdaemon.readthedocs.io/en/latest/)

## Option som gælder for de fleste add-on, som jeg normalt aktiverer
* Start on boot: Make the add-on start during a system boot
* Watchdog: This will start the add-on if it crashes
* Auto update: Auto update the add-on when there is a new version available
* Show in sidebar: Add this add-on to your sidebar 

## File editor Configuration:
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

## ESPHome
* Nyhere 20210616 [Power up your ESP-based projects](https://www.youtube.com/watch?v=du38Oir_xp8)
  * We're launching new tools to make it easier for new users to start with any projects running on the ESP8266 and ESP32. [Blog version:](https://www.home-assistant.io/blog/2021/06/16/power-up-your-esp-projects/)


## Samba share Configuration
* Option: workgroup (required): Change WORKGROUP to reflect your network needs.
* Option: username (required): The username you would like to use to authenticate with the Samba server.
* Option: password (required): The password that goes with the username configured for authentication.
* Option: allow_hosts (required): List of hosts/networks allowed to access the shared folders.
```
workgroup: WORKGROUP
username: izoehhuzhaqefrhx
password: Gjq9e7UepXn6RJna
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
### Åben Samba share fra Arbejdsplads PC's stifinder
* Vælg Andre steder --> Forbind til server -->
* Udfyld felt: smb://izoehhuzhaqefrhx@homeassistant.local/config --> Klik Tilslut -->
* indtast password når du bliver spurgt
  
## MariaDB 
* Start med at se denne video [Home Assistant MariaDB Install and System Monitoring](https://www.youtube.com/watch?v=FbFyqQ3He7M) fra [Everything Smart Home](https://www.youtube.com/channel/UCrVLgIniVg6jW38uVqDRIiQ)
### Configuration
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
    password: z8wvgwg3thwhqnfc
rights:
  - username: homeassistant
    database: homeassistant
```
* /config/configuration.yaml
```
# Home Assistant MariaDB Install and System Monitoring https://www.youtube.com/watch?v=FbFyqQ3He7M
recorder:
  db_url: !secret maria_db
```
* /config/secrets.yaml
  * for ikke at have vores password i configuration.yaml, hvor vi nemt kan komme til at dele dem med andre opretter dette entry i /config/secrets.yaml
```
# MariaDB
maria_db: mysql://homeassistant:lsjqg8ha@core-mariadb/homeassistant?charset=utf8mb4
```
## System Monitoring
  * System Monitoring /config/configuration.yaml
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
  * System Monitoring Lovelace
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

* Configuration
* Option: log_level: The log_level option controls the level of log output by the addon and can be changed to be more or less verbose, which might be useful when you are dealing with an unknown issue. Possible values are:
  * trace: Show every detail, like all called internal functions.
  * debug: Shows detailed debug information.
  * info: Normal (usually) interesting events.
  * warning: Exceptional occurrences that are not errors.
  * error: Runtime errors that do not require immediate action.
  * fatal: Something went terribly wrong. Add-on becomes unusable.
* Please note that each level automatically includes log messages from a more severe level, e.g., debug also shows info messages. By default, the log_level is set to info, which is the recommended setting unless you are troubleshooting.  
Using trace or debug log levels puts the SSH and Terminal daemons into debug mode. While SSH is running in debug mode, it will be only able to accept one single connection at the time.
* Option group ssh: The following options are for the option group: ssh. These settings only apply to the SSH daemon.
  * Option ssh: username: This option allows you to change to username the use when you log in via SSH. It is only utilized for the authentication; you will be the root user after you have authenticated. Using root as the username is possible, but not recommended.  
  * Option ssh: password: Sets the password to log in with. Leaving it empty would disable the possibility to authenticate with a password. We would highly recommend not to use this option from a security point of view.  
  **Note: The password will be checked against HaveIBeenPwned. If it is listed, the add-on will not start.**
  * Option ssh authorized_keys: Add one or more public keys to your SSH server to use with authentication. This is the recommended over setting a password.  
  Please take a look at the awesome documentation created by GitHub about using public/private key pairs and how to create them.  
  * Option ssh: sftp: When set to true the addon will enable SFTP support on the SSH daemon. Please only enable it when you plan on using it.  
  Note: Due to limitations, you will need to set the username to root in order to be able to enable the SFTP capabilities.
  * Option ssh: compatibility_mode: This SSH add-on focusses on security and has therefore only enabled known secure encryption methods. However, some older clients do not support these. Setting this option to true will enable the original default set of methods, allowing those clients to connect.   
  Note: Enabling this option, lowers the security of your SSH server!
  * Option ssh: allow_agent_forwarding: Specifies whether ssh-agent forwarding is permitted or not.  
  Note: Enabling this option, lowers the security of your SSH server! Nevertheless, this warning is debatable.
  * Option ssh: allow_remote_port_forwarding: Specifies whether remote hosts are allowed to connect to ports forwarded for the client.  
  Note: Enabling this affects all remote forwardings, so think carefully before doing this.
  * Option ssh: allow_tcp_forwarding: Specifies whether TCP forwarding is permitted or not. 
  Note: Enabling this option, lowers the security of your SSH server! Nevertheless, this warning is debatable.
* Shared settings : The following options are shared between both the SSH and the Web Terminal.
  * Option: zsh: The add-on has ZSH pre-installed and configured as the default shell. However, ZSH might not be your preferred choice. By setting this option to false, you will disable ZSH and the add-on will fallback to Bash instead.
  * Option: share_sessions: By default, the terminal session between the web client and SSH is shared. This allows you to pick up where you left your terminal from either of those. This option allows you to disable this behavior by setting it to false, which effectively sets SSH to behave as it used to be.
  * Option: packages: Allows you to specify additional Alpine packages to be installed in your shell environment (e.g., Python, Joe, Irssi).   
  Note: Adding many packages will result in a longer start-up time for the add-on.
  * Option: init_commands: Customize your shell environment even more with the init_commands option. Add one or more shell commands to the list, and they will be executed every single time this add-on starts.
  * Option: i_like_to_be_pwned: Adding this option to the add-on configuration allows to you bypass the HaveIBeenPwned password requirement by setting it to true.
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

## HACS
* Start med at se denne video [How to install HACS in 2021 in Home Assistant - NEW UPDATED VERSION!](https://www.youtube.com/watch?v=D6ZlhE-Iv9E) af [Smart Home Junkie](https://www.youtube.com/channel/UCVtQ4AOSmCFUuvixddYiSxw)

1. Åben ssh terminal og indstat følgende komando:
```
~ wget -q -O - https://install.hacs.xyz | bash - 
```   
2. Restart Homeassistant
3. Ryd browserdata 
4. Gå nu til Homeassistant Configuration --> Integrations --> ADD INTEGRATION -->
5. Søg for HACS --> Install
6. Select alle 4 options --> Submit
7. 
```
/config/custom_components
```

## Zigbee
Her er nogke videoer:

* 20201028 [How-to ZigBee in Home Assistant](https://www.youtube.com/watch?v=2Nn0u4ACsx0)
* 20201115 [IKEA Zigbee remotes - upgrading CC2531 firmware](https://www.youtube.com/watch?v=n8Qfyfkvt14&t=27s)


## Telegram
Se videoen fra Average Automation [Home Assistant Telegram notification setup guide.](https://www.youtube.com/watch?v=sHdWirJ2v8M&t=71s)
* [Home Assistant Telegram manual: ](https://www.home-assistant.io/integrations/telegram)
* [Telegram Bot Manual: ](https://core.telegram.org/bots#6-botfather)

### Huskeliste for ny bot:

1. The **name** of your bot is displayed in contact details and elsewhere.
2. The **Username** is a short name, to be used in mentions and t.me links. Usernames are 5-32 characters long and are case insensitive, but may only include Latin characters, numbers, and underscores. Your bot's username must end in 'bot', e.g. 'tetris_bot' or 'TetrisBot'.
3. The **token** (api_key) is a string along the lines of 110201543:AAHdqTcvCH1vGWJxfSeofSAs0K5PALDsaw that is required to authorize the bot and send requests to the Bot API. Keep your token secure and store it safely, it can be used by anyone to control your bot.

4. Print denne huske liste og udfyld den inden du starter:

* BOT
   * name: HaSekt
   * Username: HaSekt_bot
   * token (api_key): 110201543:AAHdqTcvCH1vGWJxfSeofSAs0K5PALDsaw

* NOTIFIER_NAME:
  * User 1:
    * username: NOTIFIER_sekt
    * Chat_ID: 123456789
  * User 2:
    * username: NOTIFIER_noo
    * Chat_ID: 234567890
  * User n+1:
    * username: NOTIFIER_noo
    * Chat_ID: 345678901

* NOTIFIER_NAME_OF_GROUP
  * Group 1:
    * beskrivelse:  tyveri alarm gruppe
    * groupname:    NOTIFIER_GROUP_burglary
    * Chat_ID:      -987654321
  * Group 2:
    * beskrivelse:  oversvømmelse alarm gruppe
    * groupname:    NOTIFIER_GROUP_flood
    * Chat_ID:      -876543210
  * Group n+1:
    * beskrivelse:
    * groupname:
    * Chat_ID:

### Configuration:
Her er en eksemple installation, brug oplysningerne fra dit skema og tilpas til dine behov.:  
**config/configuration.yaml**
```
# Example configuration.yaml entry for the Telegram Bot
telegram_bot:
  - platform: polling
    api_key: !secret ha-sekt_token
    allowed_chat_ids:
      - CHAT_ID_1 # example: 123456789 for the chat_id of a user
      - CHAT_ID_2 # example: -987654321 for the chat_id of a group
      - CHAT_ID_3

# Example configuration.yaml entry for the notifier
notify:
  - platform: telegram
    name: NOTIFIER_NAME
    chat_id: CHAT_ID_1

  # It is possible to add multiple notifiers by using another chat_id
  # the example belows shows an additional notifier which sends messages to the bot which is added to a group
  - platform: telegram
    name: NOTIFIER_NAME_OF_GROUP
    chat_id: CHAT_ID_2

```
tilføj nu en linie idin secret.yaml fil og brug din egen token (api_key):  
**config/secrets.yaml**
```
ha-sekt_token: 110201543:AAHdqTcvCH1vGWJxfSeofSAs0K5PALDsaw
```

# [Opdeling af konfigurationen](https://www.home-assistant.io/docs/configuration/splitting_configuration/)

* Configuration.yaml
  * secrets.yaml
  * automations.yaml
  * groups.yaml
  * lights.yaml
  * scenes.yaml
  * scripts.yaml