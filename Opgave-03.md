# Opgave-03 - Byg en ESP32-kontakt med relæ og signal indikator
OK, Du har nu oprettede konfigurationsfilen til ESP32-kontakten. Det har dog kun nogle grundlæggende indstillinger. Din software vil bare oprette forbindelse til din WiFi og intet andet. 
Så du bliver nødt til at redigere konfigurationsfilen og tilføje et par flere komponenter. For eksempel styre relæet ved at trykke på ESP32-kontakten.

## Forbind dit ESP32 Kort som vist på billederne  
Forbinder du nu de 2 LED og trykknappen til din ESP32, kan vi bruge den røde Led til at simulere et relæ og den grønne til at vise forbindelse status med og bruge trykknappen som tænd og sluk kanp.

![Opgaver-01_bb.png](/Images/Opgaver-01_bb.png) 

### Ledninger tilsluttes som følger:
1. De hvide stifter ved LED forbindes til sorte stifter ved ESP32 (stel)
2. Den røde stift forbindes til ESP32 GPIO12 
3. Den grønne stift forbindes til ESP32 GPIO13
4. En hvide stift fra trykknap forbindes til sorte stifter ved ESP32 (stel)
5. En hvid stift fra trykknap forbindes til ESP32 GPIO0

## Tilføj komponenter til konfigurationsfilen
Lad os gennemgå nogle af de tilgængelige indstillinger, som du kan tilføje.  
Klik på **[EDIT]** for at åbne konfigurationsfilen og indtaste følgende **nederst i filen**:
```
binary_sensor:
  - platform: gpio
    pin:
      number: GPIO0
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
* binary_sensor: Udføres hvergang ESP32-kontakten bliver påvirket 
* switch: Vil skifte relæet (Rød LED) til og fra
* status_led: Nyttigt til at vise status for en enhed. Fortæller dig om advarsler eller fejl
* wifi_signal sensor: Overvåger den modtagne signalstyrke
* uptime sensor: Sporer den tid (i sekunder), enheden har været online
* version text_sensor: Giver oplysninger om den aktuelle version af ESPHome-firmwaren, der er installeret på enheden.

### Save & Close filen  
Filem bliver gemt som "/config/esphome/esp32_01_sekt.yaml"

## Reprogramer din ESP32 med den nye opsætning
* Vælg den USB-port som din ESP32 er forbundet til
* Check Config, hvis ok så fortsæt med næste punkt ellers ret fejl
* Upload nu ændringer til din ESP32
* Du skal nu gerne se noget som dette:
```

```