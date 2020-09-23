# 04-Tilføj Trykknapper og Lysdioder til konfigurationsfilen

OK, Du har nu oprettede konfigurationsfilen til ESP32-kontakten. Det har dog kun nogle grundlæggende indstillinger. Din software vil bare oprette forbindelse til din WiFi og intet andet. 
Så du bliver nødt til at redigere konfigurationsfilen og tilføje et par flere komponenter. For eksempel styre relæet ved at trykke på ESP32-kontakten.

## Forbind dit ESP32 Kort som vist på billederne  
Forbinder du nu de 2 LED og trykknappen til din ESP32, kan vi bruge den Røde-Led til at simulere et relæ og den grønne til at vise forbindelse status med og bruge trykknappen som tænd og sluk kanp.

![ESP32-Kontakt_LED](/Opgaver/ESP32-Kontakt/ESP32-Kontakt_LED_bb.png) 

### Ledninger tilsluttes som følger:
1. Trykknapper
   1. En hvide stift fra hver trykknap forbindes til sorte stifter ved ESP32 (stel)
   2. En hvid stift fra trykknap_1 forbindes til ESP32 GPIO4
   3. En hvid stift fra trykknap_2 forbindes til ESP32 GPIO0
2. Lysdioder
   1. Den Røde stift fra Røde Lysdiode forbindes til en af de Røde stifter ved ESP32 (+3,3V)
   2. Den Grønne stift fra Grønne Lysdiode forbindes en af de til Røde stifter ved ESP32 (+3,3V)
   3. Den Hvide stift fra den Røde Lysdiode forbindes til ESP32 GPIO14 
   4. Den Hvide stift fra den Grønne Lysdiode forbindes til ESP32 GPIO12

## Tilføj komponenter til konfigurationsfilen
De første komponenter vi vil tilføje er vores trykknapper, trykknapper er af typen [GPIO Binary Sensor](https://esphome.io/components/binary_sensor/gpio.html), herunder er vist koden: 
```
binary_sensor:
  - platform: gpio
    pin:
      number: GPIO4
      mode: INPUT_PULLUP
      inverted: True
    name: "Trykknap 1"

  - platform: gpio
    pin:
      number: GPIO0
      mode: INPUT_PULLUP
      inverted: True
    name: "Trykknap 2"

```
Næste komponent vi tilføjer er den Røde lysdiode, den Røde lysdiode vælger jeg at oprette som et [Switch Component](https://esphome.io/components/switch/index.html), herunder er vist koden:
```
switch:
  - platform: gpio
    name: "Rød Lysdiode"
    pin: 
      number: GPIO14
      inverted: yes
    id: RedLed
```
Sidste komponent vi tilføjer nu er vores Grønne Lysdiode, den Grønne Lysdiode vælger jeg at bruge som [Status LED](https://esphome.io/components/status_led.html), herunder er vist koden:
```
status_led:
  pin:
    number: GPIO12
    inverted: yes
```
Vi har nu tilføjet vores komponenter, den kan nu betjenes fra vores [http://homeAssistant.local:8123](http://homeassistant.local:8123/lovelace/default_view), men vi kan ikke tænde og slukke vores Lysdiode fra trykkanp_1 for at få denne funktion skal vi tilføje en handling til bores Trykknap_1, koden er vist herunder:
```
binary_sensor:
  - platform: gpio
    pin:
      number: GPIO4
      mode: INPUT_PULLUP
      inverted: True
    name: "Trykknap 1"
    on_press:
      - switch.toggle: RedLed
```
Vi har nu oprettet kode til de komponenter som vi selv har tilføjet vores udviklings_print, der er dog 3 komponenter mere som følger med ESPHome
*  [WiFi Signal Sensor](https://esphome.io/components/sensor/wifi_signal.html)
*  [WiFi Info Text Sensor](https://esphome.io/components/text_sensor/wifi_info.html)
*  [Uptime Sensor](https://esphome.io/components/sensor/uptime.html)  
*  [Version Text Sensor](https://esphome.io/components/text_sensor/version.html)  
herunder ses koden for disse 4 sensor:
```
sensor:
  - platform: wifi_signal
    name: "Desk light WiFi signal"
    update_interval: 60s

  - platform: uptime
    name: "Desk light uptime"

text_sensor:
  - platform: wifi_info
    ip_address:
      name: ESP IP Address
    ssid:
      name: ESP Connected SSID
    bssid:
      name: ESP Connected BSSID
    mac_address:
      name: ESP Mac Wifi Address

  - platform: version
    name: "Desk light ESPHome version"
```
Nu har vi alt den kode vi skal bruge for nu, Klik på **[EDIT]** for at åbne konfigurationsfilen og indtaste følgende **nederst i filen**:

```
binary_sensor:
  - platform: gpio
    pin:
      number: GPIO4
      mode: INPUT_PULLUP
      inverted: True
    name: "Trykknap 1"
    on_press:
      - switch.toggle: RedLed

  - platform: gpio
    pin:
      number: GPIO0
      mode: INPUT_PULLUP
      inverted: True
    name: "Trykknap 2"

switch:
  - platform: gpio
    name: "Rød Lysdiode"
    pin: 
      number: GPIO14
      inverted: yes
    id: RedLed

status_led:
  pin:
    number: GPIO12
    inverted: yes

sensor:
  - platform: wifi_signal
    name: "Desk light WiFi signal"
    update_interval: 60s

  - platform: uptime
    name: "Desk light uptime"

text_sensor:
  - platform: wifi_info
    ip_address:
      name: ESP IP Address
    ssid:
      name: ESP Connected SSID
    bssid:
      name: ESP Connected BSSID
    mac_address:
      name: ESP Mac Wifi Address

  - platform: version
    name: "Desk light ESPHome version"

```
### Save & Close filen  
Filem bliver gemt som "/config/esphome/esp32_01_sekt.yaml"

## Reprogramer din ESP32 med den nye opsætning
* Check Config, hvis ok så fortsæt med næste punkt ellers ret fejl
* Upload nu ændringer til din ESP32 via tty (/dev/ttyUSB0....)
Herunder ses resultatet:
![Oversigt](/Opgaver/ESP32-Kontakt/Oversigt.png) 
