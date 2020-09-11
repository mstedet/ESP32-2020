# Opgave-03 - Byg en ESP32-kontakt med relæ og signal indikator
OK, så du oprettede konfigurationsfilen til ESP32-kontakten. Det har dog kun nogle grundlæggende indstillinger. Hvis du skulle blinke firmwaren til ESP32-kontakten nu, ville den bare oprette forbindelse til din WiFi og intet andet. Så du bliver nødt til at redigere konfigurationsfilen og tilføje et par flere komponenter. For eksempel skifteindstillingerne til at styre relæet for at tænde og slukke for ESP32-kontakten.

## Forbind dit ESP32 Kort som vist på billederne  
![Opgaver-01_bb.png](/Images/Opgaver-01_bb.png) 

### Ledninger tilsluttes som følger:
1. De hvide stifter ved LED forbindes til sorte stifter ved ESP32 (stel)
2. Den røde stift forbindes til ESP32 GPIO-12 
3. Den grønne stift forbindes til ESP32 GPIO-13
4. En hvide stift fra trykknap forbindes til sorte stifter ved ESP32 (stel)
5. En hvid stift fra trykknap forbindes til ESP32 GPIO-2

## Tilføj komponenter til konfigurationsfilen
Lad os gennemgå nogle af de tilgængelige indstillinger, som du kan tilføje.  
Klik på **[EDIT]** for at åbne konfigurationsfilen og indtaste følgende **nederst i filen**:
```
binary_sensor:
  - platform: gpio
    pin:
      number: GPIO2
      mode: INPUT_PULLUP
      inverted: True
    name: "Desk light button"
    on_press:
      - switch.toggle: relay

switch:
  - platform: gpio
    name: "Desk light relay"
    pin: GPIO12
    id: relay

status_led:
  pin:
    number: GPIO13
    inverted: yes

sensor:
  - platform: wifi_signal
    name: "Desk light WiFi signal"
    update_interval: 60s

  - platform: uptime
    name: "Desk light uptime"

text_sensor:
  - platform: version
    name: "Desk light ESPHome version"
```
* binary_sensor: Checks for anytime the button on the ESP32-kontakten is pressed 
* switch: Would trigger the relay on and off 
* status_led: Useful to show the status of a device. Letting you know of any warning or errors 
* wifi_signal sensor: Monitors the received signal strength
* uptime sensor: Tracks the time (in seconds) the device has been online
* version text_sensor: Provides information of the current version of the ESPHome firmware installed on the device